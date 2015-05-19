# Approximate Subgraph Matching - Relation Extraction

Code for performing Relation Extraction using the Approximate Subgraph Matching algorithm
Based originally on the NICTA VRL submission to BioNLPST-13.

## Building

Use Maven:

	$ mvn compile
  
For this to work you'll need appropriate dependencies installed in some Maven repository you can read:

* [ClearNLP with text span tracking](https://code.google.com/r/admackin-clearnlp-spans/)
* JSBD adapted to use Maven (readbiomed jsbd project)
* ESM version 1.1 (not 1.0 -- readbiomed esm project)


## Running Experiments

Create a new directory, and set the environment variables:

* `TRAINING`: points to the directory containing unparsed `.txt` and `.a1`/`.a2` files
* `TEST`: the same, for the test directory
* `CONFIG`: points to the ClearNLP config - you probably just want to use 
  `/PATH/TO/asm-re/src/main/resources/configure/config_en_dep-craft-fromraw.xml`

It's convenient to set up a file `config_vars` in the experiment directory to
set these, and then source that from your helper scripts using '.'

To parse,you'll need to download [the relevant ClearNLP models](https://code.google.com/p/clearnlp/wiki/TrainedModelsOld), which should be stored at `/PATH/TO/asm-re/model`. The above config file assumes you have:

* `dictionary-1.2.0.zip`
* `craft-en-pos-1.1.0g.jar`
* `craft-en-dep-1.1.0b1.jar`

You can then run `asm-re/src/main/scripts/parse-and-move.sh`
To learn rule patterns, call `asm-re/src/main/scripts/infer-rules.sh`

So assuming you have `../shared-scripts` symlinked to
`/PATH/TO/asm-re/src/main/scripts`, 
in the experiment directory, you might have a file `parse.sh`:

	#!/bin/sh
	. config_vars
	../shared-scripts/parse-and-move.sh

And `infer-rules.sh`:

	#!/bin/sh
	. config_vars
	../shared-scripts/run-rule-inference.sh

After running `./infer-rules.sh`, the rules should end up in `./training/inferred-rules`
