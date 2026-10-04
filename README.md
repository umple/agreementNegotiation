# Agreement Negotiation

This repository contains tools related to the domain of qualitative agreement negotiation. Qualitative agreements are dominated by text, often many thousands of lines of such text, divided into sections and subsections at various levels of granularity. Top level sections are often called 'Articles'. At the bottom level there are usually 'Clauses'. These sections have various numbering schemes.

Examples of qualitative negotiations include those for international treaties (climate change, trade, arms, etc.), labour-management agreements (usually called collective agreements), and many kinds of legal agreements.

This repository does not focus on forms of negotation that mostly revolve around amounts of money (quantitative negotiation), since there are are already many tools for such negotiations.

This repository has been created for the PhD thesis work of Emmanuel Ayeleso. When his thesis is submitted, a link will be added here, most likely towards the end of 2023.

## Metamodel

The negotiation metamodel captures the core data needed for managing qualititative negotiations among many parties.

It is designed to form the database and internal model for qualitative negotiation tools.

## Parser

This tool, currently a prototype., will be able to parse textual contracts such as treaties and collective agreement and enable negotiation of changes. The plan is to populate the metamodel


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
cd ../src
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
