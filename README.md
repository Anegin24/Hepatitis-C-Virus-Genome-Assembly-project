# Viral Genome Assembly Project
### dependencies
```bash
bwa
samtools
bedtools
unicycler
bandage
```
### Testing pipeline for assembly HCV genome (9600bp). In this project I'm trying to assembly fragment 1 of HCV genome (length 5400bp)
```bash
bwa mem ref/reftype1.fasta HCVB/L86Y3-20240822-HCV-B_S14_L001_R1_001.fastq.gz HCVB/L86Y3-20240822-HCV-B_S14_L001_R2_001.fastq.gz | samtools view -h -b -o HCVB.bam
samtools view -b -F 0xc HCVB.bam -o HCVB.filtered.bam
samtools sort -@ 20 -n HCVB.filtered.bam -o HCVB.sorted.n.bam
samtools fixmate -m HCVB.sorted.n.bam HCVB.fixmate.bam
samtools sort -@ 20 HCVB.fixmate.bam -o HCVB.sorted.p.bam
samtools markdup -r -@ 20 HCVB.sorted.p.bam HCVB.dedup.bam
samtools index HCVB.dedup.bam 
samtools sort -n -o HCVB.dedup.sorted.bam HCVB.dedup.bam
bedtools bamtofastq -i HCVB.dedup.sorted.bam -fq HCVB.dedup.R1.fastq -fq2 HCVB.dedup.R2.fastq
gzip HCVB.*fastq
unicycler -1 HCVB/HCVB.dedup.R1.fastq.gz -2 HCVB/HCVB.dedup.R2.fastq.gz -l ref/reftype1.fasta -t 20 -o unicyclerhybird_HCVB --keep 3
```
### Code easy but my strength knowledge in molecular biology,genomics and biology more important to finish this project!!!
