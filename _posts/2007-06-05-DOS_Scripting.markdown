---
layout: post 
title: DOS Scripting
---

### Accepting Arguments

Use %1 from within the script as the first argument and %2 as the second
etc. If the argument is a filename then the following can be used
instead to process it:

    %1 is the normal parameter. Returns filename exactly as passed. 

    %~f1 expands %1 to the drive, path, and file name. If passed only filename from current directory, this will expand it. 

    %~d1 extracts (or expands then extracts) the drive letter from %1 

    %~p1 extracts (or expands then extracts) the path from %1 

    %~dp1 extracts (or expands then extracts) the drive letter and path from %1 

    %~sp1 extracts (or expands then extracts) the short path from %1 

    %~n1 extracts (or expands then extracts) the file name, without extension, from %1 

    %~sn1 extracts (or expands then extracts) the short file name, without extension, from %1 

    %~x1 extracts (or expands then extracts) the file extension from %1 

    %~nx1 extracts (or expands then extracts) the file name and extension from %1 

    %~sx1 extracts (or expands then extracts) the short extension from %1 

\%0 is the complete path, filename, and extension of the script itself.

### Timing

#### Wait for a program to finish

Your batch file runs a Windows program, but you need it to not do
anything else until after that Windows program finishes. The general
answer is to use the START command with the /WAIT option like this:

`  start /wait notepad.exe`

However this does not work for programmes lke compressed-executables.

#### Make a time dealy

The \"Wscript.Sleep\" command allows you to specify a sleep time in
milliseconds. Here is batch code for a ten-second delay that creates the
needed scripting file:

    @echo off
    echo Starting!
    echo Wscript.Sleep 10000> sleep.vbs
    start /w wscript.exe sleep.vbs
    echo Done!
    del sleep.vbs

### Network

#### Find expired hosts in an input file

This can be used to find expired hosts in etc\\\\hosts:

    @echo off

    :: Test to see if we are on Win 9x by how ampersands are handled
    > HostsExpired.tmp echo 1234&rem
    type HostsExpired.tmp | find "rem" > nul
    if errorlevel 1 goto NOT9X
    goto ISWIN9X

    :NOT9X
    if exist HostsExpired.tmp del HostsExpired.tmp
    echo This batch file will read the HOSTS file looking for
    echo machine names that don't have a DNS "A" entry. A list 
    echo of those machines will be appended to a file named
    echo "HostsExpired.txt" in the default directory (usually
    echo the same directory the batch file is in).

    :: Wake the system up by pinging the primary DNS
    call :PINGDNS

    :: now read the first two words in each line of the HOSTS file
    if not exist %windir%\\System32\\drivers\\etc\\hosts goto DONE
    for /f "tokens=1,2" %%x in (%windir%\\System32\\drivers\\etc\\hosts) do call :TESTLINE %%x %%y
    goto DONE

    :TESTLINE
    :: Arguments (dirty) - IP, MachineName
    :: Did we get two arguments (was it a blank line)?
    if [%2]==[] goto DONE
    :: Is it a commented line?
    echo %1 | find "#" > nul
    if not errorlevel 1 goto DONE
    :: Do a NS lookup. If "Address" shows up twice, it is good.
    nslookup -type=A %2 2>nul | find /c "Address" | find "2" > nul
    if errorlevel 1 call :TESTAGAIN %1 %2
    echo %2
    goto DONE

    :TESTAGAIN
    :: Arguments (clean) - IP, MachineName
    :: Use ping as a time delay in case NS needed more time to 
    :: look up or in case my !@#$%?! DHCP lease expired again.
    call :PINGDNS
    :: Do a NS lookup. If "Address" shows up twice, it is good.
    nslookup -type=A %2 2>nul | find /c "Address" | find "2" > nul
    if errorlevel 1 call :LOG %1 %2
    goto DONE

    :LOG
    :: Arguments (clean) - IP, MachineName
    :: Add the IP/name entry to the list.
    echo %1    %2>> HostsExpired.txt
    goto DONE

    :PINGDNS
    :: Used as a delay or to wake up the system by pinging the primary DNS.
    :: Read the ipconfig command and separate things by the colon.
    for /f "tokens=1,2 delims=:" %%x in ('ipconfig /all') do call :PINGDNS2 "%%x" %%y

    :PINGDNS2
    :: Arguments (dirty) - IpconfigEntry, IpconfigValue
    :: If %1 (the beginning of the ipconfig line) has "DNS Servers"
    :: in it, then %2 (the end of the ipconfig line) has the DNS IP.
    echo %1 | find "DNS Servers" > nul
    if errorlevel 1 goto DONE
    :: Ping the DNS server, but limit the hop count so we *probably* will
    :: get out of our local network, but *probably* won't harrass the DNS.
    ping -i 4 %2 > nul
    ping -i 4 %2 > nul
    goto DONE

    :ISWIN9X
    if exist HostsExpired.tmp del HostsExpired.tmp
    echo This batch file requires Windows NT or newer. 
    goto DONE

    :DONE

#### Get IP address

NT/2000/XP:

`  ipconfig.exe | find "IP Address" | find /v " 0.0.0.0"`

9X:

`  winipcfg.exe /batch %temp%\\winipcfg.out`\
`  type %temp%\\winipcfg.out | find "IP Address" | find /v " 0.0.0.0"`

Although this works on both but does it in a different way:

`  ping.exe -n 1 -i 1 -w 1 www.microsoft.com`\
`  arp.exe -a | find "Interface"`

If the IP is required by itself then it can be filted using for
tokens/delims:

`  ipconfig | find "IP Address" > ip1.txt`\
`  for /f "tokens=1-2 delims=:" %i in (ip1.txt) do echo %j> ip2.txt`\
`  for /f "tokens=1-3 delims=." %i in (ip2.txt) do echo %i.%j.%k.21> ip3.txt`

It would be a nightmare trying to do this on Win 9x are it does not have
for natively.

### Windows

#### Get user name

This exports the key from the reg and gets the value from it into a env
variable:

    @echo off
    start /w regedit /e reg.txt HKEY_LOCAL_MACHINE\\System\\CurrentControlSet\\control
    type reg.txt | find "Current User" > "Current#User.bat"
    echo set CurrentUser=%%1>"Current User.bat"
    call "Current#User.bat"
    del "Current?User.bat" > nul
    del reg.txt > nul
    echo %CurrentUser%
    exit

This gives the username in quotes though, although it can be removed by
making it to a file like this:

    md temp1
    cd temp1
    :: creates a temp1 directory for the batch file to work in.  Essentially
    :: just a directory that doesn't contain any files.
    :: HERES THE IMPORTANT BIT:-
    echo hello>%username%
    :: echos hello into a file called "Bert"
    :: DOS can't call the file "bert", so it drops the quotes on each side....
    :: ...giving you a directory with one file in it  (called bert)
    dir /B >c:\\workingdirectory\\user.txt
    :: outputs the data to a file called user.txt in the working directory
    deltree temp1
    :: just a quick tidy up.

Or use the NET config command to create a batch file with the output of
the \'User name\' line and grab the third \'parameter\':

    @echo off
    :: The "net config" generates several lines of data, among
    :: them one that has my user name like this
    :: User name       EPHELPS
    :: I put just that line into a temporary batch file
    net config workstation | find "User" > temp.bat
    :: Since the first word in my temporary batch file is "User",
    :: I'll need to create a batch file named user. The user.bat
    :: file will have the word "name" as it's first argument
    :: and the word "EPHELPS" as it's second argument. I'm 
    :: obviously after the second argument here!
    echo set value=%%2> user.bat
    :: Now I call my temp.bat which will in turn run user.bat
    call temp.bat
    :: Delete the temporary files we made
    del temp.bat
    del user.bat
    :: Display the value we got!
    echo Your user name is %value%

Instead of \'net config workstation\' only \'net config\' is required
under Win 9x.

The following uses DEBUG instead:

    @echo off
    :: Parses the output of the "net config" command to get
    :: the user name. Uses debug to trim
    :: away all unwanted info from the response line.
    set value=
    :: Use net config to get lots of data, then filter it
    net config | find "User name" > setvalue.bat
    :: Use DEBUG to overwrite the beginning data
    >  script echo e 0100 "                     set value="
    >> script echo w
    >> script echo q
    debug setvalue.bat < script > nul
    del script
    call setvalue.bat
    del setvalue.bat
    echo User name is %value%

### See Also

[Process Lines of Data Using
FOR](http://www.ericphelps.com/batch/lines/word-for.htm)

[Processing Lists](http://www.ericphelps.com/batch/lists/index.htm)

[More Proessing Lists](http://www.ericphelps.com/batch/nt/lists.txt)

[Get User Input](http://www.ericphelps.com/batch/userin/index.htm)

[Stupid DOS Tricks](http://www.ericphelps.com/batch/tricks/index.htm)

[Joseph Hayes Tips](http://www.ericphelps.com/batch/samples/jhayes.txt)
