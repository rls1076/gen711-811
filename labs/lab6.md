---
title: "Lab 6"
author: "Jeffrey Miller"
date: "2026 Feb 27"
output: pdf_document
---


### Today
1. Review, fastqc
2. Redirection and pipes lesson
3. Script writing

## review
which for programs
conda environments
chmod for permissions
fastqc


## keypoints
Employ the grep command to search for information within files.
Print the results of a command to a file.
Construct command pipelines with two or more stages.
Use for loops to run the same command for several input files.


## questions for practical
How can I search within files?
How can I combine existing commands to do new things?

grep -A1 -h '^@SRR' *fastq | grep -v '^--" | grep -v '^@SRR'

## HELP: Nucleotide abbreviations
The four nucleotides that appear in DNA are abbreviated A, C, T and G. Unknown nucleotides are represented with the letter N. An N appearing in a sequencing file represents a position where the sequencing machine was not able to confidently determine the nucleotide in that position. You can think of an N as being aNy nucleotide at that position in the DNA sequence.


## Exercise 1

1. Search for the sequence `GNATNACCACTTCC` in the `SRR098026.fastq` file.
  Have your search return all matching lines and the name (or identifier) for each sequence
  that contains a match.

  grep -B1 "GNATNACCACTTCC" SRR098026.fastq

2. Search for the sequence `AAGTT` in both FASTQ files.
  Have your search return all matching lines and the name (or identifier) for each sequence
  that contains a match.

  grep -B1 "AAGTT" *.fastq

3. How do the search results differ when matching in one file vs. both files? If you wanted to keep the original FASTQ format, how would you get around this?

4. Make a file called 'bad-reads.fastq' made up of reads with 10 Ns or more in a row. 

grep -B1 -A2 'NNNNNNNNNN' SRR098026.fastq > bad-reads.fastq

## Exercise 2

How many sequences are there in `SRR098026.fastq`? Remember that every sequence is formed by four lines.

wc -l SRR098026.fastq
Divide the count by 4, so 996/4 = 249

## Exercise 3

How many sequences in `SRR098026.fastq` contain at least 3 consecutive Ns? 249 sequences

grep NNN SRR098026.fastq | wc -l
249 sequences

## Exercise 4

Print the file prefix of all of the `.txt` files in our current directory.



## Exercise 5

After renaming the fastqs as demonstrated, remove `_2026` from all of the `.txt` files.

for filename in *.fasta
do
echo -e name=$(basename ${filename} .fastq)
echo -e mv ${filename} ${name}_2026.txt
done

## Exercise 6

We want the script to tell us when it's done.

1. Open `bad-reads-script.sh` and add the line `echo "Script finished!"` after the `grep` command and save the file.
2. Run the updated script.

for name in *.fastq 
do 
echo ${name} 
done

(above is the same as saying
echo SRR097977.fastq
echo SRR098026.fastq)

for fq in *.fastq
do 
wc -l ${fq}
done

for filename in *.fastq
do
head -n 2 ${filename}
done


To set a variable: FOO='this-is-a-var'
To assess a variable: eacho $FOO

## keypoints

- `grep` is a powerful search tool with many options for customization.
- `>`, `>>`, and `|` are different ways of redirecting output.
- `command > file` redirects a command's output to a file.
- `command >> file` redirects a command's output to a file without overwriting the existing contents of the file.
- `command_1 | command_2` redirects the output of the first command as input to the second command.
- `for` loops are used for iteration.
- `basename` gets rid of repetitive parts of names.





```bash
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/004/SRR2589044/SRR2589044_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/004/SRR2589044/SRR2589044_2.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/003/SRR2584863/SRR2584863_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/003/SRR2584863/SRR2584863_2.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/006/SRR2584866/SRR2584866_1.fastq.gz
curl -O ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR258/006/SRR2584866/SRR2584866_2.fastq.gz
```
```bash
$ cd
$ wget ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt
```

or

```bash
$ cd
$ curl -O ftp://ftp.ensemblgenomes.org/pub/release-37/bacteria/species_EnsemblBacteria.txt
```