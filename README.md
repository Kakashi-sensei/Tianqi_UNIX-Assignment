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

