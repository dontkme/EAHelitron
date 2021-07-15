# EAHelitron    
<img src="https://github.com/dontkme/PersonalScripts/raw/master/helitron-mini-01.png"  align="right" />

[![releaseVersion](https://img.shields.io/badge/release%20version-1.5.3-green.svg?style=flat)](https://github.com/dontkme/EAHelitron) [![Last-changedate](https://img.shields.io/badge/last%20change-2021--06--25-green.svg)](https://github.com/dontkme/EAHelitron/commit) ![perlVersion](https://img.shields.io/badge/perl-%3E%3D5.10-blue.svg?sytle=flat)


Easy to Annotate Helitrons Unix-like command line.              

EAHelitron is written by Perl. Use the Helitron conservative structure traits: 5’ terminal with TC, 3’ terminal with CTAGt and before CTAG 2-10 nt has an GC-rich hairpin loop. We use the Perl regular expression (RE) engine and its Embedded-Code Construct to find out all matched results, then print and convert to a GFF3 format file. Using the gff3 file made above, we can visualize these Helitrons in genome visualization tools such as IGV, Gbrowse, and Jbrowse, and easily characterize the captured genes.

EAHelitron is an unix-like program, you can run it on all Perl 5.10+ supported machines and write the command in your shell script. Linux, Mac OS and Windows test passed.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine.

### Prerequisites

Make sure you have Perl on your system.
Enter these words in your system terminal.
```
perl -v
```
If the terminal displays Perl version information, then we can download all EAHelitron files. 
https://github.com/dontkme/EAHelitron/archive/refs/tags/v1.5.3.zip


### Installing


if you downloaded the zip, unzip the EAHelitron-1.5.3.zip


```
unzip EAHelitron-1.5.3.zip
```

And enter the decompressed folder, run EAHelitron.

```
cd EAHelitron-1.5.3
perl EAHelitron -h
```

If the screen displays help information. It worked.

## Running 

Example: Predict Helitrons and search for their 5' TC terminals within 20,000 bp upstream.
```
perl EAHelitron –o testEAHout –u 20000 teat.fas
```
Or 

```  
./EAHelitron –o testEAHout –u 20000 teat.fas
```   
Options:
        
         [-o string|outprefix Default: EAHeli_out]
         [-u int|upstream length Default: 3000]
         [-d int|downstream length Default: 500]
         Advanced options:
         [-T string|TC pattern. User's 5'TC pattern]
         [-H string|Hairpin pattern. User's Hairpin left pattern]
         [-r int[0-5]|CTRRt 3' terminal fuzzy level;
                 0: CTAGT
                 1: CT[AG]GT
                 2: CTA[AG]T
                 3: CT[AG]{2}T
                 4: CT[AG]{2}.{1}
                 5: CTAG.{1}
                 Default: 0]

We also provide EAHelitron_P, a multi-threaded version that can speed up running in a large genome.

(Need Perl Parallel::ForkManager. You could install it by command: cpan Parallel::ForkManager )

```
perl EAHelitron_P –p 8 –o testEAHout –u 20000 teat.fas
```
-p: How many threads to use. It is recommended not to exceed the number of sequences contained in the fasta file you input.

Advanced options. Users can enter their own pattern (Perl RE) to predict Helitrons.
(Warning: Advanced options may significantly increase the false positive rate, only for exploration).

-H: Use Hairpin left sequnce pattern:
```
perl EAHelitron_P –p 8 -H "GC" –o testEAHout_H_GC teat.fas
```

-T: Use TC pattern:
```
perl EAHelitron_P –p 8 -T "TC" –o testEAHout_T_TC teat.fas
```

Or use in combination:
```
perl EAHelitron_P –p 8 -T "TC" -H "GC" –o testEAHout_T_H teat.fas
```
-r: CTRRt 3' terminal fuzzy level:
6 fuzzy levels of CTRRt terminal [0-5]

```
perl EAHelitron_P –p 8 -r 3 –o testEAHout_r3 teat.fas
```

The outputs named EAHout.3.txt EAHout.5.txt EAHout.5.fa EAHout.gff3 EAout.u20000.fas. (prefix 'EAHout' could be set by –o option, 20000 is your –u option value). 

*.3.txt: All 3’ terminal sequences with a 10nt left flank and a 4nt right flank in fasta format. All sequences named by its local chromosome name, a 'H' means Helitron, '.3' suffix to mark they are 3’ terminals. The minus strain terminal have a 'tr' prefix. (e.g. Chr1H10.3, trChr5H40.3).

*.5.txt: All 5’terminal sequences which were matched in the 3’ terminal’s upstream sequences, with a 5 nt left flank and a 20 nt right flank. The name of sequences have .5.1 suffix to mark they are 5’ terminal and the match orders numbers. (e.g. Chr1H10.5.1,trChr5H40.5.2) 

*.5.fa: Possible full-length Helitron sequences which start with 5’ terminal and end with 3’ terminal. (Only for Helitrons)

*.u*.fas: All 3’ terminal upstream sequences.  

*.d*.fas: All 3’ terminal downstream sequences.

*.gff3: Helitron location information in GFF3 format.

*.bed: Helitron 3'-ends location in bed format.

*.len.txt: Summary of genome sequences length, Helitron counts and Helitron Densities

## History

(EAHelitron)v1.5300 2021/06/25 Add feature. User TC pattern and hairpin left seuqence pattern options.

(EAHelitron)v1.5200 2020/09/25 Use new regular expression, which based on BioPerl, to get chromosome names, in order to adapt to more cases. Thanks to [Darcy Jones](https://github.com/darcyabjones)'s advice.

(EAHelitron)v1.5100 2019/06/10 Add feature. Output a BED of 3’-ends.  (*.bed)

(EAHelitron)v1.5000 2019/03/08 Add feature. Output a summary of genome sequences length, Helitron counts and Helitron Densities. (*.len.txt)

(EAHelitron)v1.4000 2018/08/31 Add CTAGT fuzzy level [0-5] option.

(EAHelitron)v1.3100 2017/09/19 Add snp switch.

(EAHelitron)v1.3000 2017/08/29 Add downstream feature.

...

(EAHelitron)v1.0000 2016/09/22 first version upload to GitHub.

## Authors

**Hu Kaining** - *Initial work* - [dontkme](https://github.com/dontkme)

## License
![licence](https://img.shields.io/github/license/mashape/apistatus.svg?maxAge=2592000)

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details


