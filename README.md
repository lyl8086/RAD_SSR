RAD-seq-Assembly-Microsatellite
---
<strong>Codes used in microsatellites discovery of overlapping paired-end RAD seq.</strong>

Please cite our paper if you find it useful to your work.

>Xue DX, Li YL, Liu JX (2017), A rapid and cost-effective approach for the development of polymorphic microsatellites 
in non-model species by using paired-end RAD sequencing. <em>Molecular Genetics and Genomics</em>.

PREREQUISITES
---
* [CAP3](http://seq.cs.iastate.edu/cap3.html)

* [STACKS](http://catchenlab.life.illinois.edu/stacks/)

* [QDD3](http://net.imbe.fr/~emeglecz/qdd_download.html)

Steps:
---
Step1. Clustering the reads (containing enzyme sites) by STACKS.
```
ustacks
cstacks
sstacks
```
Step2. Export paired-end reads (random sheared) into seperate fasta files.
```
sort_read_pairs.pl
```
Step3. Run local assembly.
```
CP3_Opti.pl
```
<strong>*The above steps can be accomplished by a easy used pipeline soft [RADassembly](https://github.com/lyl8086/RADscripts/tree/master/RADassembly/Pipeline)</strong>

Step4. Check the assembled contigs, retain high quality contigs.
```
bwa mem
samtools view
samtools view -hf 0x2 -F 0x100 -q 20 bamfile | awk '$6 !~/H|S/ && $0 !~/XA:Z:/ && $0 !~/SA:Z:/' | samtools view -bS - >final.QC.bam
extract contigs id from the above QC bam file, then you get the final high quality contigs
```
Step5. Run QDD in galaxy or in command line, please refer to the [manuals](http://net.imbe.fr/~emeglecz/QDDweb/QDD-3.1.2/Documentation_QDD-3.1.2.pdf)
```
perl QDD.pl
```

---

Then you get the microsatellites from assembled contigs(including primers)

<h3>All the above steps can be accomplished in a pipeline soft RAD_SSR (under development)</h3>

* Please [contact](mailto:liyulong12@mails.ucas.ac.cn) me if you have any questions
