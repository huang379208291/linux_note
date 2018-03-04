# step1: download data

```
python gener_cmd_srr.py  SRR_Acc_List.txt > step1_wget_cmd.sh

wget ftp://ftp-trace.ncbi.nih.gov//sra/sra-instant/reads/ByRun/sra/SRR/SRR176/SRR1761523/SRR1761523.sra
wget ftp://ftp-trace.ncbi.nih.gov//sra/sra-instant/reads/ByRun/sra/SRR/SRR176/SRR1761522/SRR1761522.sra
wget ftp://ftp-trace.ncbi.nih.gov//sra/sra-instant/reads/ByRun/sra/SRR/SRR176/SRR1761521/SRR1761521.sra
wget ftp://ftp-trace.ncbi.nih.gov//sra/sra-instant/reads/ByRun/sra/SRR/SRR176/SRR1761520/SRR1761520.sra
wget ftp://ftp-trace.ncbi.nih.gov//sra/sra-instant/reads/ByRun/sra/SRR/SRR176/SRR1761519/SRR1761519.sra
wget ftp://ftp-trace.ncbi.nih.gov//sra/sra-instant/reads/ByRun/sra/SRR/SRR176/SRR1761518/SRR1761518.sra

```

# step2: format conversion

```
python gener_cmd_sra2fq.py  SRR_Acc_List.txt 

/home/xie186/test_ara/software/sratoolkit.2.8.2-1-ubuntu64/bin/fastq-dump --split-files SRR1761523.sra
/home/xie186/test_ara/software/sratoolkit.2.8.2-1-ubuntu64/bin/fastq-dump --split-files SRR1761522.sra
/home/xie186/test_ara/software/sratoolkit.2.8.2-1-ubuntu64/bin/fastq-dump --split-files SRR1761521.sra
/home/xie186/test_ara/software/sratoolkit.2.8.2-1-ubuntu64/bin/fastq-dump --split-files SRR1761520.sra
/home/xie186/test_ara/software/sratoolkit.2.8.2-1-ubuntu64/bin/fastq-dump --split-files SRR1761519.sra
/home/xie186/test_ara/software/sratoolkit.2.8.2-1-ubuntu64/bin/fastq-dump --split-files SRR1761518.sra

```

# step3: build index and align the reads



```
## Get the test data
head -1000 SRR1761523_1.fastq > test_1.fq
head -1000 SRR1761523_2.fastq > test_2.fq
## build index (you don't need to generate the index multiple times.)
hisat2-build ara_ref.fasta ara_ref.fasta
## Align the reads to reference genome
hisat2 -x ara_ref.fasta -1 test_1.fq -2 test_2.fq > test.sam 

```

