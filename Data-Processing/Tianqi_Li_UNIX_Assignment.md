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
$ egrep "ZMMLR|ZMMIL|ZMMMR|Sample_ID" fang_et_al_genotypes.txt > maize_fang_et_al_genotypes.txt && egrep "ZMPBA|ZMPIL|ZMPJA|Sample_ID" fang_et_al_genotypes.txt > teosinte_fang_et_al_genotypes.txt && awk -f transpose.awk teosinte_fang_et_al_genotypes.txt > teosinte_transposed_genotypes.txt && awk -f transpose.awk maize_fang_et_al_genotypes.txt > maize_transposed_genotypes.txt && mkdir Data-Processing && sed -i '1,3d' maize_transposed_genotypes.txt teosinte_transposed_genotypes.txt && sed '1d' snp_position.txt > snp_position_nohead.txt sort -k1,1V snp_position_nohead.txt > snp_position_nohead_sorted.txt && sort -k1,1V maize_transposed_genotypes.txt > maize_transposed_genotypes_sorted.txt && sort -k1,1V teosinte_transposed_genotypes.txt > teosinte_transposed_genotypes_sorted.txt && join -1 1 -2 1 snp_position_nohead_sorted.txt maize_transposed_genotypes_sorted.txt > maize_transposed_genotypes_joined.bed && join -1 1 -2 1 snp_position_nohead_sorted.txt teosinte_transposed_genotypes_sorted.txt > teosinte_transposed_genotypes_joined.bed
```

By inspecting this file I learned that:

*  egrep can grep mutiple conditions and build a new file
*  AWK script can transpose both files 'maize and teosinte'
*  Also, a new folder of 'Data-Processing' is necessary
*  All unnecessary headlines shall be deleted because different items cannot 'join' in a sigle line as head line
*  join sorted files, there must be a same column

##Data Processing

###Teosinte Data

```
sort -k2,2 teosinte_transposed_genotypes_joined.bed > teosinte_transposed_genotypes_joined_chr.bed
```

sort teosinte by chromsoms order 'column 2'



```
$ grep -v "^#" teosinte_transposed_genotypes_joined_chr.bed | cut -f2 | uniq -c #count chro
```
    output

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

1.  It means we can split this in different lines
2.  However, if we can rename all chromosomes from numbers into words it would be easier to split

```
$ sed -n '1,155p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr1.bed
```
```
$ sed -n '156,208p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr10.bed
```
```
$ sed -n '209,335p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr2.bed
```
```
$ sed -n '336,442p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr3.bed
```
```
$ sed -n '443,533p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr4.bed
```
```
$ sed -n '534,655p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr5.bed
```
```
$ sed -n '656,731p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr6.bed
```
```
$ sed -n '732,828p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr7.bed
```
```
$ sed -n '829,890p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr8.bed
```
```
$ sed -n '891,950p' teosinte_transposed_genotypes_joined_chr.bed > teosinte_transposed_genotypes_joined_chr9.bed
```
```
$ sed -n '951,956p' teosinte_transposed_genotypes_joined_chr.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_transposed_genotypes_joined_mutiple.bed
```
```
$ sed -n '957,983p' teosinte_transposed_genotypes_joined_chr.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_transposed_genotypes_joined_unknown.bed
```

1.  Chromosomes of mutiple and unknown were sent to final folder
2.  10 files were built, and each one was in the same chromosome

```
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr9.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr9_ordered_increased.bed
```
```
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr8.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr8_ordered_increased.bed
```
```
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr7.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr7_ordered_increased.bed
```
```
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr6.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr6_ordered_increased.bed
```
```
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr5.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr5_ordered_increased.bed
```
```
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr4.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr4_ordered_increased.bed
```
```
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr3.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr3_ordered_increased.bed
```
```
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr2.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr2_ordered_increased.bed
```
```
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr1.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr1_ordered_increased.bed
```
```
$ sort -k3,3V teosinte_transposed_genotypes_joined_chr10.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr10_ordered_increased.bed
```

1.  All files were sorted in increased order
2.  All files were saved in final folder

```
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr8.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr8_ordered_decreased.bed
```
```
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr1.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr1_ordered_decreased.bed
```
```
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr2.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr2_ordered_decreased.bed
```
```
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr3.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr3_ordered_decreased.bed
```
```
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr4.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr4_ordered_decreased.bed
```
```
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr5.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr5_ordered_decreased.bed
```
```
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr6.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr6_ordered_decreased.bed
```
```
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr7.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr7_ordered_decreased.bed
```
```
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr9.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr9_ordered_decreased.bed
```
```
$ sed 's/?/-/g' teosinte_transposed_genotypes_joined_chr10.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_chr10_ordered_decreased.bed
```
1.  All files were sorted in desearsed order and all '?' were changed into '-'
2.  g was used to change all '?', otherwise, only '?' before '/' would be changed


###Maize Data

```
$ sort -k2,2 maize_transposed_genotypes_joined.bed > maize_transposed_genotypes_joined_chr.bed
```
Sort in chromosome orders "2 column"

```
$ sed -n '1,155p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr1.bed
```
```
$ sed -n '156,208p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr10.bed
```
```
$ sed -n '209,335p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr2.bed
```
```
$ sed -n '336,442p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr3.bed
```
```
$ sed -n '443,533p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr4.bed
```
```
$ sed -n '534,655p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr5.bed
```
```
$ sed -n '656,731p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr6.bed
```
```
$ sed -n '732,828p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr7.bed
```
```
$ sed -n '829,890p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr8.bed
```
```
$ sed -n '891,950p' maize_transposed_genotypes_joined_chr.bed > maize_transposed_genotypes_joined_chr9.bed
```
```
$ sed -n '951,956p' maize_transposed_genotypes_joined_chr.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_transposed_genotypes_joined_mutiple.bed
```
```
$ sed -n '957,983p' maize_transposed_genotypes_joined_chr.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_transposed_genotypes_joined_unknown.bed
```

Same as teosinte, the file was splitted into 12 parts

```
$ sort -k3,3V maize_transposed_genotypes_joined_chr9.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr9_ordered_increased.bed
```
```
$ sort -k3,3V maize_transposed_genotypes_joined_chr8.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr8_ordered_increased.bed
```
```
$ sort -k3,3V maize_transposed_genotypes_joined_chr7.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr7_ordered_increased.bed
```
```
$ sort -k3,3V maize_transposed_genotypes_joined_chr6.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr6_ordered_increased.bed
```
```
$ sort -k3,3V maize_transposed_genotypes_joined_chr5.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr5_ordered_increased.bed
```
```
$ sort -k3,3V maize_transposed_genotypes_joined_chr4.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr4_ordered_increased.bed
```
```
$ sort -k3,3V maize_transposed_genotypes_joined_chr3.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr3_ordered_increased.bed
```
```
$ sort -k3,3V maize_transposed_genotypes_joined_chr2.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr2_ordered_increased.bed
```
```
$ sort -k3,3V maize_transposed_genotypes_joined_chr1.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr1_ordered_increased.bed
```
```
$ sort -k3,3V maize_transposed_genotypes_joined_chr10.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr10_ordered_increased.bed
```

Sort in increased order of 10 files

```
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr8.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr8_ordered_decreased.bed
```
```
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr1.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr1_ordered_decreased.bed
```
```
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr2.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr2_ordered_decreased.bed
```
```
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr3.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr3_ordered_decreased.bed
```
```
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr4.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr4_ordered_decreased.bed
```
```
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr5.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr5_ordered_decreased.bed
```
```
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr6.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr6_ordered_decreased.bed
```
```
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr7.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr7_ordered_decreased.bed
```
```
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr9.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr9_ordered_decreased.bed
```
```
$ sed 's/?/-/g' maize_transposed_genotypes_joined_chr10.bed | sort -k3,3nr > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_chr10_ordered_decreased.bed
```
decreasing position values and with missing data encoded by this symbol: '-'


###debug


```
$ rm -rf teosinte_transposed_genotypes_joined_mutiple.bed maize_transposed_genotypes_joined_mutiple.bed
```

```
$ cd ..
```

```
$ grep “mutiple” teosinte_transposed_genotypes_joined.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_transposed_genotypes_joined_mutiple.bed
```

```
$ grep “mutiple” maize_transposed_genotypes_joined.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_transposed_genotypes_joined_mutiple.bed
```

```
$ cd Data-Processing
```

```
$ sed -i '/mutiple/d' maize_chr2_ordered_decreased.bed maize_chr2_ordered_increased.bed maize_chr4_ordered_decreased.bed maize_chr4_ordered_increased.bed maize_chr6_ordered_decreased.bed maize_chr6_ordered_increased.bed maize_chr7_ordered_decreased.bed maize_chr7_ordered_increased.bed maize_chr9_ordered_decreased.bed maize_chr9_ordered_increased.bed teosinte_chr2_ordered_decreased.bed teosinte_chr2_ordered_increased.bed teosinte_chr4_ordered_decreased.bed teosinte_chr4_ordered_increased.bed teosinte_chr6_ordered_decreased.bed teosinte_chr6_ordered_increased.bed teosinte_chr7_ordered_decreased.bed teosinte_chr7_ordered_increased.bed teosinte_chr9_ordered_decreased.bed teosinte_chr9_ordered_increased.bed
```

There are lines with 'mutiple' position. But their have chromosome numbers. This debug can fix this problem.

It is not work

I used some new way

```
$sort -k3,3V maize_transposed_genotypes_joined.bed > maize_transposed_genotypes_joined_333.bed
```
```
$ sed -n '940,956p' maize_transposed_genotypes_joined_333.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/maize_transposed_genotypes_joined_mutiple.bed
```
```
sort -k3,3V teosinte_transposed_genotypes_joined.bed > teosinte_transposed_genotypes_joined_333.bed
```
```
$ sed -n '940,956p' teosinte_transposed_genotypes_joined_333.bed > /home/tianqili/Tianqi_UNIX-Assignment/Data-Processing/teosinte_transposed_genotypes_joined_mutiple.bed
```

