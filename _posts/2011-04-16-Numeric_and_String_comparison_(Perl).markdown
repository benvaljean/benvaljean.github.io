---
layout: post 
title: Numeric and String comparison (Perl)
---

===Numeric comparison===
{| {{table}}
| ==||Equal to
|-
| !=||Not Equal to
|-
| >||Greater than
|-
| <||Less than
|-
| >=||Greater than or Equal to
|-
| <=||Less than or Equal to
|}
===String comparison===
{| {{table}}
| eq||equal
|-
| ne||not equal
|-
| =~||contains
|-
| !~||does not contain
|-
| 
|}

====Example====
Cycle through the current folder, displaying all files except those that contain "dirtest88" and excluding the "." and ".." folders.
<pre>
my $dirname = ".";
opendir(DIR, $dirname) or die "can't opendir $dirname: $!";
while (defined($file = readdir(DIR))) {
    # do something with "$dirname/$file"
    if ($file ne "." && $file !~ /dirtest88/ && $file ne "..") {
    say "There is $dirname/$file";
    }
}
closedir(DIR);
</pre>


[[Category:Perl]]
