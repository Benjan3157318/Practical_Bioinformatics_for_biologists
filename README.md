Benjan Karnebeek

e-mail: b.karnebeek@student.rug.nl

Course: Practical Bioinformatics for Biologists

Description:
The goal was to extract from a FASTA format file of a Transcritome analysis (https://bmcgenomics.biomedcentral.com/articles/10.1186/1471-2164-15-929) the following information about the contigs.

First all the headers were extracted in order to remove the information about the sequences which was not required.

Command: grep ">" raw/Marra2014_data.fasta > headers.txt

The header.txt file was used to extract further information about contigs.

Get number of contigs: wc -l headers.txt > output/contigs.txt

Get isogroups: cut -d " " -f 7 headers.txt | cut -d "p" -f 2 | sort | uniq > output/isogroups.txt

Get contig lengths: cut -d " " -f 3  headers.txt | cut -d "=" -f 2 | sort -n > output/contig_lengths.txt

Get number of reads : cut -d " " -f 5  headers.txt | cut -d "=" -f 2 | sort -n > output/reads

Finally the information was combined into a .csv file called marra.csv.

Commands: 

echo "contig,contig_length,number_of_reads,isogroup" > output/marra.csv

cat headers.txt | tr "=" " " | tr "g" " " |tr "p" " " | cut -d " " -f 2,6,9,15 | tr " " "," >> output/marra.csv
