create a java file hello world program: ie: abc.java







create a class file: which is compiled java code
javac abc.java

if a java file has annonymous inner class then one more class file with <classname>$1.class is created along-with the .class file


run java program:
java myjavafile.class
or
java myjavafile

compile a java program using another jar file:
if our .java file is using some external jar files methods etc then; mandatory to include the jar file name in -cp for compilation of the java code:
javac -cp d:\external.jar mysourcecode.java


run a java program using another jar file:
if our .class file is using some external jar files methods etc then; mandatory to include the jar file name in -cp for running the java class file:
java -cp ,;d:\external.jar mysourcecode.class
or
java -cp ,;d:\external.jar mysourcecode

shorcut way: if you DONOT want to give classpath and jar name in java command then place in location: jdk/jre/lib/ext/*.jar


path: where your binary executables are available: eg: java, javac
classpath: location where .class files are available; javac and jvm will use; program may not compile (compilation error: class not found) or program may not run (runtime error: class not found)
java: is used to run .class file
javac (java compiler): is used to create class file from .java file
jre (java runtime environment): to JUST run(execute) the java program LINE BY LINE (interpreter): JVM + Library classes
jvm (java virtual machine): inside the JRE this is responsible to run(execute) the java program: 
jdk (java development kit): to code (develop), compile (build) and execute(run) java program: JRE + Development tools
.class: byte code
.jar: collection of .class files
.war: collection of web files like: html, css, jsp, servelets etc
.ear: collection of web + enterprise components like jms and jbeans etc
java program: .class, .jar, .war, .ear
javaw (java without console output): System.out.println (console output) WITHOUT console output -- generally used to run UI based application
javaws (java web start utility): centralised control of application: javaws jnlp_url (user will always get the latest version of jar whenever it is launched)
manifest file(generally name is manifest.MF OR you can give any name): provides information about jar file; which one class out of many class files to start the execution from
jnlp_url: used with javaws eg: javaws jnlp_url
jlink: 
jshell:

development tools:
library: ??
Library classes: 
package:
class:
method:
function:
attributes: ??


jvm architecture:


public static void main

public:
private:
protected:

constant:
variable:

super():
this():

throw:
throws:

get:
post:

multithreading:
multitasking:
multiprocessing:

cpu:
cpu core:

first level caching:
second level caching:

web application:
distributed application:

jar, war, ear are nothing but zipped file

jar file (java archive file): group of class files
war file (web archive file): group of web application files ie: html, css, js, images, jsp, servelets
ear file (enterprise archive file): group of enterprise files: everything in java and j2ee eg: jbeans, jms and all web type files


all third party plugins are available in the form of jar files: eg: tomcat.jar

create jar file:
jar -cvf abc.jar a.class b.class
jar -cvf abc.jar classes/*.class

extract jar file:
jar -xvf abc.jar

view table of contents of jar file:
jar -tvf abc.jar


inject a class in jar file:



create executable jar file:
create a manifest file: manifest.MF (or can be any name): IMPORTANT that it should have new line as the last line:
Main-Class: Demo.jar

jar -cvfm demo.jar manifest.MF Demo.class Demo$1.class

how to execute an executable jar file:(generally used for GUI based application)
java -jar demo.jar

create war file:


create ear file:


download java
set JAVA_HOME
set CLASS_PATH

download ant and unzip in folder
set ANT_HOME

set JAVA_HOME, CLASS_PATH and ANT_HOME in PATH environment variable

ant uses build.xml

ant -help
ant -buildfile build.xml


rest:
soap:


