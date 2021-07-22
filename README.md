# agreementNegotiation
This tool will be able to parse textual contracts such as treaties and collective agreement and enable negotiation of changes


Steps to make the Agreement parser (and any other independent app) work

1. TO DO create a build script that will

a) copy the UmpleParser generated code into a lib directory

create directory lib if not there

```
cd lib
cp -pr /Users/tcl/umple/UmpleParser/src-gen-umple/cruise .
```

(make sure this is never committed ... put it in .gitignore)

b) Compile the umple in the src directory, directing output to src-gen-umple (later on we should adjust the umple compiler so that it can use a classpath and compile the java directly, currently done in step c)

```
umple -g Java --path ../src-gen-umple Agreement.ump
```

c) Compile the resulting Java with the correct classpath

```
javac -cp ../lib/ *.java */*.java
```


2. As in this repo, there needs to be an en.error file in the src directory that would optionally be populated with error messages that the parser analysis step would generate.

3. Execute the result (the following currently has a problem due to 
  - will try to process everything in testagreements .. needs fixing to just process specific files

in the src directory

```
java -cp '../src-gen-umple:../lib' AgreementProcessorMain ../testagreements ../../tempOutput
```
