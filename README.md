# Agreement Negotiation

This repository contains tools related to the domain of qualitative agreement negotiation. Qualitative agreements are dominated by text, often many thousands of lines of such text, divided into sections and subsections at various levels of granularity. Top level sections are often called 'Articles'. At the bottom level there are usually 'Clauses'. These sections have various numbering schemes.

Examples of qualitative negotiations include those for international treaties (climate change, trade, arms, etc.), labour-management agreements (usually called collective agreements), and many kinds of legal agreements.

This repository does not focus on forms of negotation that mostly revolve around amounts of money (quantitative negotiation), since there are are already many tools for such negotiations.

This repository has been created for the PhD thesis work of Emmanuel Ayeleso. When his thesis is submitted, a link will be added here, most likely towards the end of 2023.

## Metamodel

The negotiation metamodel captures the core data needed for managing qualititative negotiations among many parties.

It is designed to form the database and internal model for qualitative negotiation tools.

## Parser

This tool, currently a prototype, will be able to parse textual contracts such as treaties and collective agreement and enable negotiation of changes. The plan is to populate the metamodel


agreementParser/src/Agreement.ump is an Umple program that parses each .txt file in agreementParser/testagreements according to agreementParser/src/Agreement.grammar. It brings in Umple's rule-based parser with the single line `use lib:UmpleParser.ump;` (see the [UmpleParser README](https://github.com/umple/umple/tree/master/UmpleParser)).

To build and run it, from the root of this repository:

```
ant -f build/build.xml -Dumple.jar=<path to umple.jar>
```

The umple.jar must come from an Umple build that includes UmpleParser.ump; without `-Dumple.jar` the build uses ../umple/dist/umple.jar, from an Umple clone built next to this one. The build

1. compiles Agreement.ump to Java in agreementParser/src-gen-umple,
2. compiles that Java to agreementParser/bin, and copies there agreementParser/src/en.error, where the program can define error messages of its own,
3. runs `java -cp ../bin AgreementProcessorMain ../testagreements ../../tempOutput` in agreementParser/src, where the parser finds Agreement.grammar.

For each agreement the program prints the clauses it found, or why it could not read or parse it, and it exits with a nonzero status if any agreement failed or Agreement.grammar cannot be read. It does not write to the output directory yet.

In an agreement each clause starts on a line of its own with its identifier (`Article 1`, `Section 1.1`, or a number such as `1.1.1`) followed on the same line by its heading; the lines up to the next clause are its body text. A line that starts like an identifier, with a number after `Article` or `Section` or on its own, followed by a dot, a space or the end of the line, must be a complete identifier with a heading.

`ant -f build/build.xml -Dumple.jar=<path to umple.jar> test` runs the program on agreementParser/testagreements and on the agreements in agreementParser/test, including malformed ones and ones it cannot read, and checks its exit status and its output against the .expected files there.
