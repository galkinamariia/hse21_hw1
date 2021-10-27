# hse21_hw1
# Обязательная часть задания
```
$ ls /usr/share/data-minor-bioinf/assembly/* | xargs -tI{} ln -s {} 
```
```
$ seqtk sample -s 10052001 oil_R1.fastq 5000000 > PE1.fq
$ seqtk sample -s 10052001 oil_R2.fastq 5000000 > PE2.fq
$ seqtk sample -s 10052001 oilMP_S4_L001_R1_001.fastq 1500000 > MP1.fq
$ seqtk sample -s 10052001 oilMP_S4_L001_R2_001.fastq 1500000 > MP2.fq
```
```
$ rm *.fastq
$ ls -1 | xargs -tI{} fastqc {}
$ mkdir fastqc_raw
$ ls *.html -1 | xargs -tI{} mv -v {} fastqc_raw
$ ls *.zip -1 | xargs -tI{} mv -v {} fastqc_raw
$ multiqc fastqc_raw -o multiqc_raw
```
![image](https://user-images.githubusercontent.com/59726719/139101778-10b7f989-49fe-47a7-98c5-3e6703eb87e3.png)

![fastqc_sequence_counts_plot](https://user-images.githubusercontent.com/59726719/139101371-d915f4f8-6300-4081-bccd-7ce747274c3e.png)

![fastqc_per_base_sequence_quality_plot](https://user-images.githubusercontent.com/59726719/139101869-1031ccd5-0afb-4cc5-acc3-e3935b09aedb.png)

![fastqc_per_sequence_quality_scores_plot](https://user-images.githubusercontent.com/59726719/139101939-bcf1b091-b3ca-4809-a744-b839947a7267.png)

![fastqc_per_sequence_gc_content_plot](https://user-images.githubusercontent.com/59726719/139102137-933c33ea-0a3e-4653-8927-f8ac5383d192.png)

![fastqc_per_base_n_content_plot](https://user-images.githubusercontent.com/59726719/139102408-35ccd046-d8bf-4134-b03b-453626ae5e81.png)

![fastqc_sequence_duplication_levels_plot](https://user-images.githubusercontent.com/59726719/139102462-ee30c45e-aecc-49c3-8051-39fe7d16ddda.png)

![fastqc_adapter_content_plot](https://user-images.githubusercontent.com/59726719/139102543-9d5d3c4c-f7f2-425c-b720-61ca090acb68.png)

```
$ platanus_trim PE1.fq PE2.fq
$ platanus_internal_trim MP1.fq MP2.fq
$ rm *.fq
```
```
$ mkdir fastqc_trimmed
$ ls *trimmed -1 | xargs -tI{} fastqc {} -o fastqc_trimmed
$ multiqc fastqc_trimmed -o multiqc_trimmed
```
![image](https://user-images.githubusercontent.com/59726719/139102734-3a05d685-2df9-4081-8d74-e6cd2e6b7069.png)

![fastqc_sequence_counts_plot (1)](https://user-images.githubusercontent.com/59726719/139102791-484af75d-c81a-47de-a651-6ad1ae932927.png)

![fastqc_per_base_sequence_quality_plot (1)](https://user-images.githubusercontent.com/59726719/139102871-e546f7d0-fe7d-4f85-a371-23e52fd33c17.png)

![fastqc_per_sequence_quality_scores_plot (1)](https://user-images.githubusercontent.com/59726719/139102934-6e5b3e93-9ab6-4de9-9bc6-be8e1ed5def0.png)

![fastqc_per_sequence_gc_content_plot (2)](https://user-images.githubusercontent.com/59726719/139103029-f1ac7a89-0fa1-433c-a1b8-a47562cfdbe4.png)

![fastqc_per_base_n_content_plot (1)](https://user-images.githubusercontent.com/59726719/139103127-27e747fe-b218-46db-be3a-6cf3008bff01.png)

![fastqc_sequence_length_distribution_plot](https://user-images.githubusercontent.com/59726719/139103200-2affbad0-6deb-4b97-9991-52d0133e7dc7.png)

![fastqc_sequence_duplication_levels_plot (1)](https://user-images.githubusercontent.com/59726719/139103256-911f6f94-4c6e-40f4-9de4-472347e881f1.png)

![fastqc_adapter_content_plot (1)](https://user-images.githubusercontent.com/59726719/139103310-7927c4be-6383-4483-9812-2414dd858919.png)

```
$ screen -S mashishkin_1_assemble
$ bash
$ platanus assemble -o Poil -f PE1.fq.trimmed PE2.fq.trimmed 2> assemble.log
$ platanus scaffold -o Poil -c Poil_contig.fa -IP1 PE1.fq.trimmed PE2.fq.trimmed -OP2 MP1.fq.int_trimmed $ MP2.fq.int_trimmed 2> scaffold.LOGFILE
$ platanus gap_close -o Poil -c Poil_scaffold.fa -IP1 PE1.fq.trimmed PE2.fq.trimmed -OP2 MP1.fq.int_trimmed $ MP2.fq.int_trimmed 2> gap_close.log
$ rm *trimmed
```
