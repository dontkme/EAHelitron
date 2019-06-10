# EAHelitron    
<img src="https://github.com/dontkme/PersonalScripts/raw/master/helitron-mini-01.png"  align="right" />

[![releaseVersion](https://img.shields.io/badge/release%20version-1.5.1-green.svg?style=flat)](https://github.com/dontkme/EAHelitron) [![Last-changedate](https://img.shields.io/badge/last%20change-2019--03--08-green.svg)](https://github.com/dontkme/EAHelitron/commit) ![perlVersion](https://img.shields.io/badge/perl-%3E%3D5.10-blue.svg?sytle=flat)

Easy to Annotate Helitrons Unix-like command line.              

EAHelitron is written by Perl. Used the helitron conversed structure traits: 5’ terminal with TC, 3’ terminal with CTAGt and before CTAG 2-10 nt has an GC-rich hairpin loop. We used the Perl regular expression engine and its Embedded-Code Construct to find out all matched results, then print and convert to a GFF3 format file. Using the gff3 file made above, we can visual these helitrons in IGV, Gbrowse, Jbrowse and other kind of genome visualization tools, and character the captured genes easily.

EAHelitron is an unix-like program you can run it in all Perl5.10+ supported machines and write the command in your shell script. Linux and Windows test passed.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine.

### Prerequisites

Make sure your system has Perl.
Type these word into your system terminal.
```
perl -v
```
If has the Perl version information, we download all EAHelitron files. https://github.com/dontkme/EAHelitron/archive/master.zip


### Installing

Unzip the EAHelitron-master.zip


```
unzip EAHelitron-master.zip
```

And enter the unzipped fold, run EAHelitron.

```
cd EAHelitron-master
perl EAHelitron -h
```

If the screen shows the help information. It woked.

## Running 

Explain how to run the EAHelitron for this system
```
perl EAHeliton –o testEAHout –u 20000 teat.fas
```
OR 

```  
./EAHeliton –o testEAHout –u 20000 teat.fas
```   
Options:
        
         [-o string|outprefix Default: EAHeli_out]
         [-u int|upstream length Default: 3000]
         [-d int|downstream length Default: 500]
         [-r int[0-5]|CTRRt 3' terminal fuzzy level;
                 0: CTAGT
                 1: CT[AG]GT
                 2: CTA[AG]T
                 3: CT[AG]{2}T
                 4: CT[AG]{2}.{1}
                 5: CTAG.{1}
                 Default: 0]

We also provide EAHelitron_P a Multi-Threading version to speed up the program running with big genome. 
(Need Perl Parallel::ForkManager . You can install it by command: capn Parallel::ForkManager )

```
perl EAHeliton_P –p 8 –o testEAHout –u 20000 teat.fas
```
-p means how many threads you want to use. Suggest not bigger than the sequenced numbers your input fasta format file contained.

The out put has five files, named EAHout.3.txt EAHout.5.txt EAHout.5.fa EAHout.gff3 EAout.u20000.fas. (EAHout could be you –o option set prefix, 20000 could be you set –u option value). 

*.3.txt file contains all 3’ terminal sequences and 10nt left flank, 4nt right flank in fasta format. All sequences named by it local chromosome name, a ”H” means helitron, their matched course and a “.3” suffix to mark they are 3’ terminal sequences. The minus strain terminal have a “tr” prefix.(Like Chr1H10.3, trChr5H40.3).

*.5.txt file contains all 5’terminal sequences which were matched in 3’ terminal’s upstream with 5nt left flank and 20nt right flank. The sequences’ name have .5.1 suffix to mark they are 5’ terminal and the match number.(Chr1H10.5.1,trChr5H40.5.2). 

*.5.fa file contain the matched helitron whole sequence which start with the 5’ terminal and end with 3’ terminal.

*.u*.fas contain all 3’ terminal upstream sequences.  

*.gff3 contain the helitron location information in GFF3 format.

## History

(EAHelitron)v1.5100 2019/06/10 Add feature. Output a BED of 3’-ends.  (*.bed)

(EAHelitron)v1.5000 2019/03/08 Add feature. Output a summary of genome sequences length, Helitron counts and Helitron Densities. (*.len.txt)

(EAHelitron)v1.4000 2018/08/31 Add CTAGT fuzzy level [0-5] option.

(EAHelitron)v1.3100 2017/09/19 Add snp swich.

(EAHelitron)v1.3000 2017/08/29 Add downstream feature.

...

(EAHelitron)v1.0000 2016/09/22 fist version upload to GitHub.

## Authors

**Hu Kaining** - *Initial work* - [dontkme](https://github.com/dontkme)

## License
![licence](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details


