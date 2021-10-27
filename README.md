# hse21_hw1
$ ls /usr/share/data-minor-bioinf/assembly/* | xargs -tI{} ln -s {}

$ seqtk sample -s 10052001 oil_R1.fastq 5000000 > PE1.fq
$ seqtk sample -s 10052001 oil_R2.fastq 5000000 > PE2.fq
$ seqtk sample -s 10052001 oilMP_S4_L001_R1_001.fastq 1500000 > MP1.fq
$ seqtk sample -s 10052001 oilMP_S4_L001_R2_001.fastq 1500000 > MP2.fq


