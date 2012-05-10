---
layout: post 
title: Getting started with Java Jars and Classes
---

#### What is a Java Class?

A Java class is a branch of code which be referred to by the creation of
new objects in Java. From a narrow point of view it can be called a sub,
but a class is more flexible.

<http://docs.oracle.com/javase/tutorial/java/concepts/class.html>

#### What is a Java Jar

A jar is a collection of java code and metadata into an archive,
normally a zip.

#### Working with classes and Jars

In this example a class for converting farenheit to celcius is created
with java code that references it and is placed into a Jar:

-   Create TempratureConvertorBean.java

<!-- -->

    package tconvert;
    public class TempratureConvertorBean {
      private double celsius = 0.0;
      private double fahrenheit = 32.0;
      public double getCelsius() {
        return celsius;
      }
      public void setCelsius(double c) {
        celsius = c;
        fahrenheit = 1.8*c + 32.0;
      }
      public double getFahrenheit() {
        return fahrenheit;
      }
      public void setFahrenheit(double f) {
        fahrenheit = f;
        celsius = (f-32.0)/1.8;
      }
      public String getInfo() {
        return new String("Temp Convert Bean");
      }
    }

-   Create class subfolder
-   Compile the code into a java class into the \'class\' subfolder:
    `javac -d class TempratureConvertorBean.java`
-   Create a jar from the class:
    `jar cvf tconvert.jar -C class tconvert`
-   View contents:

<!-- -->

    $ jar tf tconvert.jar
    META-INF/
    META-INF/MANIFEST.MF
    tconvert/
    tconvert/TempratureConvertorBean.class

-   Create F2C.java

<!-- -->

    import tconvert.TempratureConvertorBean;
    public class F2C {
       public static void main(String[] arg) {
          TempratureConvertorBean b = new TempratureConvertorBean();
          double f = 0.0;
          if (arg.length>0) f = Double.parseDouble(arg[0]);
          b.setFahrenheit(f);
          double c = b.getCelsius();
          System.out.println("Fahrenheit = "+f);
          System.out.println("Celsius = "+c);
          System.out.println(b.getInfo());
       }
    }

-   Add this code to the existing jar file:
    `javac -classpath tconvert.jar F2C.java`

At this point the jar file cannot be executed by itself as the class has
to be called for it to become an executable jar. If an attempt to
execute is attempted now the following error occurs:

    $ java -jar tconvert.jar 60.0
    Failed to load Main-Class manifest attribute from tconvert.jar

An attribute must be added to the manifest pointing to our code.

#### Creating executable Jars

For the above example:

-   Create fs\_f2c.txt

<!-- -->

    Main-Class: F2C

-   Add it to the jar

<!-- -->

    $ jar uvmf fs_f2c.txt tconvert.jar F2C.class
    updated manifest
    adding: F2C.class(in = 956) (out= 578)(deflated 39%)

-   The har can now be executed standalone

<!-- -->

    $ java -jar tconvert.jar 60.0
    Fahrenheit = 60.0
    Celsius = 15.555555555555555
    Temp Convert Bean

[Category:Java](Category:Java "wikilink")
[Category:Scripting](Category:Scripting "wikilink")
