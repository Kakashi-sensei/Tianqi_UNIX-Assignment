# UNIX-Assignment
Tianqi Li
workflow for both data inspection and processing

$wc

984 lines 13198 words 82763 bytes 15 columns # words counts of snp_position.txt

2783 lines 2744038 words 11051939 byte 986 columns # words counts of fang_et_al_genotypes.txt

-rw-r--r--. 1 tianqili domain users 11051939 Sep 13 13:40 fang_et_al_genotypes.txt
-rw-r--r--. 1 tianqili domain users    82763 Sep 13 13:40 snp_position.txt

$ awk -f transpose.awk fang_et_al_genotypes.txt > transposed_genotypes.txt # transpose file of fang

$ sed 'Nd' file #delete Nline of file

-------START------

$ egrep "ZMMLR|ZMMIL|ZMMMR|Sample_ID" fang_et_al_genotypes.txt > maize_fang_et_al_genotypes.txt #grep ZMMLR or ZMMIL or ZMMMR

$ egrep "ZMPBA|ZMPIL|ZMPJA|Sample_ID" fang_et_al_genotypes.txt > teosinte_fang_et_al_genotypes.txt #grep ZMPBA, ZMPIL, and ZMPJA

$ awk -f transpose.awk teosinte_fang_et_al_genotypes.txt > teosinte_transposed_genotypes.txt
$ awk -f transpose.awk maize_fang_et_al_genotypes.txt > maize_transposed_genotypes.txt

-------easy way--------

$ sed -i '1,3d' maize_transposed_genotypes.txt teosinte_transposed_genotypes.txt #delete Sample_ID, JG_OTU, and Group lines

$ sed '1d' snp_position.txt > snp_position_nohead.txt #delete head of snp

$ sort -k1,1V snp_position_nohead.txt > snp_position_nohead_sorted.txt

$ sort -k1,1V maize_transposed_genotypes.txt > maize_transposed_genotypes_sorted.txt #sort maize
$ sort -k1,1V teosinte_transposed_genotypes.txt > teosinte_transposed_genotypes_sorted.txt #sort teosinte

$ join -1 1 -2 1 -t $'\t' snp_position_nohead_sorted.txt maize_transposed_genotypes_sorted.txt > maize_transposed_genotypes_joined.bed #join snp with maize

$ join -1 1 -2 1 -t $'\t' snp_position_nohead_sorted.txt teosinte_transposed_genotypes_sorted.txt > teosinte_transposed_genotypes_joined.bed #join snp with teosinte

$ cut -f 3 maize_transposed_genotypes_joined.bed | sed 's/1/chr1/' > maize_transposed_genotypes_chr1_full.bed #build chrom1 group
$ cut -f 3 maize_transposed_genotypes_joined.bed | sed 's/2/chr2/' > maize_transposed_genotypes_chr2_full.bed
$ cut -f 3 maize_transposed_genotypes_joined.bed | sed 's/3/chr3/' > maize_transposed_genotypes_chr3_full.bed
... ...
$ cut -f 3 teosinte_transposed_genotypes_joined.bed | sed 's/1/chr1/' > teosinte_transposed_genotypes_chr1_full.bed



-------hard way--------

$ sed -i '2,3d' maize_transposed_genotypes.txt teosinte_transposed_genotypes.txt #delete Sample_ID, JG_OTU, and Group lines

$ sort -k1,1V snp_position.txt > snp_position_sorted.bed

$ sort -k1,1V maize_transposed_genotypes.txt > maize_transposed_genotypes_sorted.bed #sort maize
$ sort -k1,1V teosinte_transposed_genotypes.txt > teosinte_transposed_genotypes_sorted.bed #sort teosinte

$ join -1 1 -2 1 snp_position_sorted.bed maize_transposed_genotypes_sorted.bed > maize_transposed_genotypes_joined.bed #join snp with maize

$ join -1 1 -2 1 -a 1 - a 2 snp_position_sorted.bed teosinte_transposed_genotypes_sorted.bed > teosinte_transposed_genotypes_joined.bed #join snp with teosinte




$ sort -k1,1V transposed_genotypes.txt > transposed_genotypes_sorted.bed
$ sort -k1,1V snp_position.txt > snp_position_sorted.bed #sort both files into .bed file

$ join -1 1 -2 1 -a 1 snp_position_sorted.bed transposed_genotypes_sorted.bed > snp_position_with_transposed_genotypes.bed #join sorted files


