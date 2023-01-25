[//]: # "#to make links in gitlab: example with racon https://github.com/isovic/racon"
[//]: # "tricks in markdown: https://openclassrooms.com/fr/courses/1304236-redigez-en-markdown"

| usage | dependencies |
| --- | --- |
| [![Nextflow](https://img.shields.io/badge/code-Nextflow-blue?style=plastic)](https://www.nextflow.io/) | [![Dependencies: Nextflow Version](https://img.shields.io/badge/Nextflow-v21.04.2-blue?style=plastic)](https://github.com/nextflow-io/nextflow) |
| [![License: GPL-3.0](https://img.shields.io/badge/licence-GPL%20(%3E%3D3)-green?style=plastic)](https://www.gnu.org/licenses) | |

<br /><br />
## TABLE OF CONTENTS


   - [AIM](#aim)
   - [CONTENT](#content)
   - [HOW TO RUN](#how-to-run)
   - [OUTPUT](#output)
   - [VERSIONS](#versions)
   - [LICENCE](#licence)
   - [CITATION](#citation)
   - [CREDITS](#credits)
   - [ACKNOWLEDGEMENTS](#Acknowledgements)
   - [WHAT'S NEW IN](#what's-new-in)

<br /><br />
## AIM



<br /><br />
## CONTENT

**ig_clustering.nf** File that can be executed using a CLI (command line interface)

**ig_clustering.config** Parameter settings for the ig_clustering.nf file

**dataset** Folder containing some datasets (batch of fasta files) than can be used as examples

**example_of_results**: folder containing examples of result obtained with the dataset.
<br /><br />
&nbsp;&nbsp;&nbsp;&nbsp;See the OUTPUT section for the description of the folder and files.

<br /><br />
## HOW TO RUN

See Protocol 136 (ask me).


### If error message

If an error message appears, like:
```
Unknown error accessing project `gmillot/ig_clustering` -- Repository may be corrupted: /pasteur/sonic/homes/gmillot/.nextflow/assets/gmillot/ig_clustering
```
Purge using:
```
rm -rf /pasteur/sonic/homes/gmillot/.nextflow/assets/gmillot*
```


### From local using the committed version on gitlab

1) Create the scm file:

```bash
providers {
    pasteur {
        server = 'https://gitlab.pasteur.fr'
        platform = 'gitlab'
    }
}
```

And save it as 'scm' in the .nextflow folder. For instance in:
\\wsl$\Ubuntu-20.04\home\gael\.nextflow

Warning: ssh key must be set for gitlab, to be able to use this procedure (see protocol 44).


2) Mount a server if required:

```bash
DRIVE="C"
sudo mkdir /mnt/share
sudo mount -t drvfs $DRIVE: /mnt/share
```

Warning: if no mounting, it is possible that nextflow does nothing, or displays a message like
```
Launching `ig_clustering.nf` [loving_morse] - revision: d5aabe528b
/mnt/share/Users
```


3) Then run the following command from here \\wsl$\Ubuntu-20.04\home\gael:

```bash
nextflow run -hub pasteur gmillot/ig_clustering -r v1.0.0
```


4) If an error message appears, like:
```
WARN: Cannot read project manifest -- Cause: Remote resource not found: https://gitlab.pasteur.fr/api/v4/projects/gmillot%2Fig_clustering
```
Make the distant repo public


5) If an error message appears, like:

```
permission denied
```

See chmod in protocol 44.


### From local using local file

Like above but then run the following command from here \\wsl$\Ubuntu-20.04\home\gael:

```bash
nextflow run ig_clustering.nf -c ig_clustering.config
```

with -c to specify the name of the config file used.


### From a cluster using a committed version on gitlab

Start with:

```bash
EXEC_PATH="/pasteur/zeus/projets/p01/BioIT/gmillot/ig_clustering" # where the bin folder of the ig_clustering.nf script is located
export CONF_BEFORE=/opt/gensoft/exe # on maestro

export JAVA_CONF=java/13.0.2
export JAVA_CONF_AFTER=bin/java # on maestro
export SINGU_CONF=singularity/3.8.3
export SINGU_CONF_AFTER=bin/singularity # on maestro
export GIT_CONF=git/2.25.0
export GIT_CONF_AFTER=bin/git # on maestro

MODULES="${CONF_BEFORE}/${JAVA_CONF}/${JAVA_CONF_AFTER},${CONF_BEFORE}/${SINGU_CONF}/${SINGU_CONF_AFTER},${CONF_BEFORE}/${GIT_CONF}/${GIT_CONF_AFTER}"
cd ${EXEC_PATH}
chmod 755 ${EXEC_PATH}/bin/*.*
module load ${JAVA_CONF} ${SINGU_CONF} ${GIT_CONF}

```

Then run:

```bash
# distant ig_clustering.nf file
HOME="${ZEUSHOME}/ig_clustering/" ; trap '' SIGINT ; nextflow run --modules ${MODULES} -hub pasteur gmillot/ig_clustering -r v1.0 -c $HOME/ig_clustering.config ; HOME="/pasteur/appa/homes/gmillot/"  ; trap SIGINT

# local ig_clustering.nf file ($HOME changed to allow the creation of .nextflow into /$ZEUSHOME/ig_clustering/. See NFX_HOME in the nextflow soft script)
HOME="${ZEUSHOME}/ig_clustering/" ; trap '' SIGINT ; nextflow run --modules ${MODULES} ig_clustering.nf -c ig_clustering.config ; HOME="/pasteur/appa/homes/gmillot/" ; trap SIGINT
```

If an error message appears, like:
```
Unknown error accessing project `gmillot/ig_clustering` -- Repository may be corrupted: /pasteur/sonic/homes/gmillot/.nextflow/assets/gmillot/ig_clustering
```
Purge using:
```
rm -rf /pasteur/sonic/homes/gmillot/.nextflow/assets/gmillot*
```

<br /><br />
## OUTPUT


**reports**: folder containing all the reports of the different processes including the *ig_clustering.config* file used.
<br /><br />
**tree.pdf**: phylogenic tree provided by BuildTrees.py and alakazam::readIgphyml.
<br /><br />
**HLP10_tree_parameters.tsv**: parameters of the phylogenic tree.
<br />
**phy_igphyml-pass.tab**: file used to draw the phylogenic tree, provided by BuildTrees.py.
<br />
**merge.tsv**: annotation of the Heavy and light chain sequences by igblast, provided by AssignGenes.py igblast and MakeDb.py igblast.
<br />
**merge_productive-F.tsv**: Failed annotations by igblast.
<br />


<br /><br />
## VERSIONS


The different releases are tagged [here](https://gitlab.pasteur.fr/gmillot/ig_clustering/-/tags)

<br /><br />
## LICENCE


This package of scripts can be redistributed and/or modified under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
Distributed in the hope that it will be useful, but without any warranty; without even the implied warranty of merchandability or fitness for a particular purpose.
See the GNU General Public License for more details at https://www.gnu.org/licenses.

<br /><br />
## CITATION


Not yet published


<br /><br />
## CREDITS


[Gael A. Millot](https://gitlab.pasteur.fr/gmillot), Hub-CBD, Institut Pasteur, Paris, France

<br /><br />
## ACKNOWLEDGEMENTS


The mentioned softwares and packages developers & maintainers

Gitlab developers

<br /><br />
## WHAT'S NEW IN


### v2.0

Conversion into DSL2 ok


### v1.0

First DSL1 version that works




