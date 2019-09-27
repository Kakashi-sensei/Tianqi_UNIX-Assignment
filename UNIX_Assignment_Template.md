#UNIX Assignment

##Data Inspection

###Attributes of `fang_et_al_genotypes`

```
$ wc fang_et_al_genotypes
```

By inspecting this file I learned that:

1. 984 lines 13198 words 82763 bytes 15 columns # words counts of snp_position.txt


###Attributes of `snp_position.txt`

```
$wc snp_position.txt
```

By inspecting this file I learned that:

*  2783 lines 2744038 words 11051939 byte 986 columns # words counts of fang_et_al_genotypes.txt

###Date prep of `snp_position.txt` and `fang_et_al_genotypes`

```
$ egrep "ZMMLR|ZMMIL|ZMMMR|Sample_ID" fang_et_al_genotypes.txt > maize_fang_et_al_genotypes.txt && egrep "ZMPBA|ZMPIL|ZMPJA|Sample_ID" fang_et_al_genotypes.txt > teosinte_fang_et_al_genotypes.txt && awk -f transpose.awk teosinte_fang_et_al_genotypes.txt > teosinte_transposed_genotypes.txt && awk -f transpose.awk maize_fang_et_al_genotypes.txt > maize_transposed_genotypes.txt && mkdir Data-Processing && sed -i '1,3d' maize_transposed_genotypes.txt teosinte_transposed_genotypes.txt && sed '1d' snp_position.txt > snp_position_nohead.txt sort -k1,1V snp_position_nohead.txt > snp_position_nohead_sorted.txt && sort -k1,1V maize_transposed_genotypes.txt > maize_transposed_genotypes_sorted.txt && sort -k1,1V teosinte_transposed_genotypes.txt > teosinte_transposed_genotypes_sorted.txt && join -1 1 -2 1 -t $'\t' snp_position_nohead_sorted.txt maize_transposed_genotypes_sorted.txt > maize_transposed_genotypes_joined.bed && join -1 1 -2 1 -t $'\t' snp_position_nohead_sorted.txt teosinte_transposed_genotypes_sorted.txt > teosinte_transposed_genotypes_joined.bed
```

By inspecting this file I learned that:

*  egrep can grep mutiple conditions and build a new file
*  AWK script can transpose both files 'maize and teosinte'
*  Also, a new folder of 'Data-Processing' is necessary
*  All unnecessary headlines shall be deleted because different items cannot 'join' in a sigle line as head line
*  join sorted files, there must be a same column

##Data Processing

###Maize Data

```
$ sort -k3,3 maize_transposed_genotypes_joined.bed > maize_transposed_genotypes_joined_chr.bed
```

sort maize by chromsoms order 'column 3'



```
$ grep -v "^#" teosinte_transposed_genotypes_joined_chr.bed | cut -f3 | uniq -c #count chro
```
    155 1
     53 10
    127 2
    107 3
     91 4
    122 5
     76 6
     97 7
     62 8
     60 9
      6 multiple
     27 unknown








###Teosinte Data

```
here is my snippet of code used for data processing
```

Here is my brief description of what this code does
