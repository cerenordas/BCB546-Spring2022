BCB546-Spring2022 - Assignment 1 - Ceren Ordas

Disclaimer: THIS README FILE IS BASICALLY ALL MY TRIAL AND ERRORS AND MY TRAIN OF THOUGHT... I DID END UP GETTING THE RIGHT THING SOONER OR LATER BUT IT WAS A BATTLE...

First got into HPC-classs and did git pull to get the assignment files:

cerenordas@Cerens-MacBook-Air ~ % ssh cordas@hpc-class.its.iastate.edu
[cordas@hpc-class ~]$ cd BCB546-Spring2022-Ceren/
[cordas@hpc-class BCB546-Spring2022-Ceren]$ ls
[cordas@hpc-class BCB546-Spring2022-Ceren]$ git status
[cordas@hpc-class BCB546-Spring2022-Ceren]$ git pull

Part 1 - 

INSPECTION OF DATA FILES:

- See first line of fang_et_al file:

head -n 1 fang_et_al_genotypes.txt 

- See the last line of the file:

tail -n 1 fang_et_al_genotypes.txt 

- less to scroll through the file:

 less -n 1 fang_et_al_genotypes.txt

- Word count for fang et al:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ wc -w fang_et_al_genotypes.txt 
2744038 fang_et_al_genotypes.txt

- Number of lines for fang et al:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ wc -l fang_et_al_genotypes.txt 
2783 fang_et_al_genotypes.txt

- Size of fang et al file:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ du -h fang_et_al_genotypes.txt 
6.5M	fang_et_al_genotypes.txt


- See first line of snp position file:

head -n 1 snp_position.txt

- See the last line of the file:

tail -n 1 snp_position.txt

- Word count for snp position file:


[cordas@hpc-class BCB546-Spring2022-Ceren]$ wc -w snp_position.txt 
13198 snp_position.txt

- Number of lines for snp position file:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ wc -l snp_position.txt 
984 snp_position.txt


- Size of snp file:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ du -h snp_position.txt 
41K	snp_position.txt



PART 2:


took heads from fangetal stuff to maise and teosinte

[cordas@hpc-class BCB546-Spring2022-Ceren]$ head -n 1 fang_et_al_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ head -n 1 fang_et_al_genotypes.txt > maise_genotypes.txt

used awk to select only stuff that had the specific groups from fangetal to get maise and teosinte genotypes

[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$3=="ZMMIL" || $3=="ZMMLR" || $3=="ZMMMR"' fang_et_al_genotypes.txt >> maise_genotypes.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi maise_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ head -n 1 fang_et_al_genotypes.txt > teosinte_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$3=="ZMPBA" || $3=="ZMPIL" || $3=="ZMPJA"' fang_et_al_genotypes.txt >> teosinte_genotypes.txt

Checked to see if the files looked like how I wanted them to:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi teosinte_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi transpose.awk 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi cut_snp.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi maise_genotypes.txt 

[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk -f transpose.awk teosinte_genotypes.txt > transposed_teosinte_genotypes.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk -f transpose.awk maise_genotypes.txt > transposed_maise_genotypes.txt


cut snp_positions to get only columns 1 3 and 4:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi snp_position.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ cut -f 1,3,4 snp_position.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ cut -f 1,3,4 snp_position.txt | head -n 5
[cordas@hpc-class BCB546-Spring2022-Ceren]$ cut -f 1,3,4 snp_position.txt > cut_snp.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi cut_snp.txt 

See where the groups I want are using grep:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ grep "ZMMIL" transposed_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ grep -w "ZMMIL" transposed_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ grep "ZMMIL" -w transposed_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ grep ZMMIL transposed_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ grep -v ZMMIL transposed_genotypes.txt 

delete rows GROUP and JG...

put headers of cut snp and transposed genotypes on a file, and join them to get header for everything
deleted headers from snps and genotypes file
took heads from fangetal stuff to maise and teosinte

[cordas@hpc-class BCB546-Spring2022-Ceren]$ head -n 1 fang_et_al_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ head -n 1 fang_et_al_genotypes.txt > maise_genotypes.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$3=="ZMMIL" || $3=="ZMMLR" || $3=="ZMMMR"' fang_et_al_genotypes.txt >> maise_genotypes.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi maise_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ head -n 1 fang_et_al_genotypes.txt > teosinte_genotypes.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$3=="ZMPBA" || $3=="ZMPIL" || $3=="ZMPJA"' fang_et_al_genotypes.txt >> teosinte_genotypes.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk -f transpose.awk teosinte_genotypes.txt > transposed_teosinte_genotypes.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk -f transpose.awk maise_genotypes.txt > transposed_maise_genotypes.txt

[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort cut_snp.txt | head -n 5
[cordas@hpc-class BCB546-Spring2022-Ceren]$ head -n 1 cut_snp.txt > header_snp.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ head -n 1 teosinte_genotypes.txt > header_teosinte.txt

[cordas@hpc-class BCB546-Spring2022-Ceren]$ join -1 1 -2 1 header_snp.txt header_teosinte.txt > header.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ head -n 1 transposed_teosinte_genotypes.txt > header_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ join -1 1 -2 1 header_snp.txt header_teosinte.txt > header.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ join -1 1 -2 1 header_snp.txt header_teosinte.txt > header.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ join -1 1 -2 1 header_snp.txt header_teosinte.txt > header.txt

[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort transposed_teosinte_genotypes.txt > sorted_teosinte_genotypes.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort cut_snp.txt > sorted_snp.txt

[cordas@hpc-class BCB546-Spring2022-Ceren]$ join -1 1 -2 1 sorted_snp.txt sorted_teosinte_genotypes.txt > joined_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -k1 transposed_teosinte_genotypes.txt > sorted_teosinte_genotypes.txt

[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -k1 cut_snp.txt > sorted_snp.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ join -1 1 -2 1 sorted_snp.txt sorted_teosinte_genotypes.txt > joined_teosinte.txt

[cordas@hpc-class BCB546-Spring2022-Ceren]$ join -1 1 -2 1 -i sorted_snp.txt sorted_teosinte_genotypes.txt > joined_teosinte.txt

check the joined teosinte, cut snp, and sorted snp:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi joined_teosinte.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi cut_snp.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ vi sorted_snp.txt 

sorted them with k1,1...

[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -k1,1 -k2,2n cut_snp.txt > sorted_snp.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -k1,1 transposed_teosinte_genotypes.txt > sorted_teosinte_genotypes.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ join -1 1 -2 1 -i sorted_snp.txt sorted_teosinte_genotypes.txt > joined_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -k1 transposed_teosinte_genotypes.txt > test.txt

display the differences in the files by comparing the files line by line:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ diff test.txt sorted_teosinte_genotypes.txt 

sort:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -k1,1 cut_snp.txt > sorted_snp.txt 
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -k1,1 transposed_teosinte_genotypes.txt > sorted_teosinte_genotypes.txt

join them:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ join -1 1 -2 1 -i sorted_snp.txt sorted_teosinte_genotypes.txt > joined_teosinte.txt

cat command used to show the contents of the file:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ cat header.txt 

FINALLY AFTER SO MUCH TRIAL AND ERROR, SHOW THE FINAL:
[cordas@hpc-class BCB546-Spring2022-Ceren]$ cat header.txt > final_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ cat joined_teosinte.txt >> final_teosinte.txt 

Sort the transposed maize genotypes and join them:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -k1,1 transposed_maise_genotypes.txt > sorted_maise_genotypes.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ join -1 1 -2 1 -i sorted_snp.txt sorted_maise_genotypes.txt > joined_maise.txt

add the header to final one:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ cat header.txt > final_maise.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ cat joined_maise.txt >> final_maise.txt

-----------------------------------------------------------------------------------------------
AFTER ALL THAT:

For final teosinte file, made 2 files, one with all SNPs with unknown positions and one with multiple positions:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$3=="unknown"' final_teosinte.txt > SNP_unknown_positions_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$3=="multiple"' final_teosinte.txt  > SNP_multiple_positions_teosinte.txt

Then did the same for maize:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$3=="unknown"' final_maise.txt > SNP_unknown_positions_maise.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$3=="multiple"' final_maise.txt > SNP_multiple_positions_maise.txt

To make 10 files for teosinte, 1 for each chromosome, with SNPs ordered in increasing position with missing data with ?:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==1' final_teosinte.txt | sort -k3,3 > chromosome1_SNP_increasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==2' final_teosinte.txt | sort -k3,3 > chromosome2_SNP_increasing_pos.teosintetxt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==3' final_teosinte.txt | sort -k3,3 > chromosome3_SNP_increasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==4' final_teosinte.txt | sort -k3,3 > chromosome4_SNP_increasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==5' final_teosinte.txt | sort -k3,3 > chromosome5_SNP_increasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==6' final_teosinte.txt | sort -k3,3 > chromosome6_SNP_increasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==7' final_teosinte.txt | sort -k3,3 > chromosome7_SNP_increasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==8' final_teosinte.txt | sort -k3,3 > chromosome8_SNP_increasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==9' final_teosinte.txt | sort -k3,3 > chromosome9_SNP_increasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==10' final_teosinte.txt | sort -k3,3 > chromosome10_SNP_increasing_pos_teosinte.txt

To make 10 more files for teosinte, 1 for each chromosome, with SNPs ordered in decreasing position with missing data with a - :

[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome1_SNP_increasing_pos_teosinte.txt | sed 's/?/-/g' > chromosome1_SNP_decreasing_pos_teosinte.txt
rdas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome2_SNP_increasing_pos_teosinte.txt | sed 's/?/-/g' > chromosome2_SNP_decreasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome3_SNP_increasing_pos_teosinte.txt | sed 's/?/-/g' > chromosome3_SNP_decreasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome4_SNP_increasing_pos_teosinte.txt | sed 's/?/-/g' > chromosome4_SNP_decreasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome5_SNP_increasing_pos_teosinte.txt | sed 's/?/-/g' > chromosome5_SNP_decreasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome6_SNP_increasing_pos_teosinte.txt | sed 's/?/-/g' > chromosome6_SNP_decreasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome7_SNP_increasing_pos_teosinte.txt | sed 's/?/-/g' > chromosome7_SNP_decreasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome8_SNP_increasing_pos_teosinte.txt | sed 's/?/-/g' > chromosome8_SNP_decreasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome9_SNP_increasing_pos_teosinte.txt | sed 's/?/-/g' > chromosome9_SNP_decreasing_pos_teosinte.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome10_SNP_increasing_pos_teosinte.txt | sed 's/?/-/g' > chromosome10_SNP_decreasing_pos_teosinte.txt

To make 10 files for maize, 1 for each chromosome, with SNPs ordered in increasing position with missing data with ?:

[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==1' final_maise.txt | sort -k3,3 > chromosome1_SNP_increasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==2' final_maise.txt | sort -k3,3 > chromosome2_SNP_increasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==3' final_maise.txt | sort -k3,3 > chromosome3_SNP_increasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==4' final_maise.txt | sort -k3,3 > chromosome4_SNP_increasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==5' final_maise.txt | sort -k3,3 > chromosome5_SNP_increasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==6' final_maise.txt | sort -k3,3 > chromosome6_SNP_increasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==7' final_maise.txt | sort -k3,3 > chromosome7_SNP_increasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==8' final_maise.txt | sort -k3,3 > chromosome8_SNP_increasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==9' final_maise.txt | sort -k3,3 > chromosome9_SNP_increasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ awk '$2==10' final_maise.txt | sort -k3,3 > chromosome10_SNP_increasing_pos_maize.txt

To make 10 more files for maize, 1 for each chromosome, with SNPs ordered in decreasing position with missing data with a - :


[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome1_SNP_increasing_pos_maize.txt | sed 's/?/-/g' > chromosome1_SNP_decreasing_pos_maize.txt

[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome2_SNP_increasing_pos_maize.txt | sed 's/?/-/g' > chromosome2_SNP_decreasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome3_SNP_increasing_pos_maize.txt | sed 's/?/-/g' > chromosome3_SNP_decreasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome4_SNP_increasing_pos_maize.txt | sed 's/?/-/g' > chromosome4_SNP_decreasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome5_SNP_increasing_pos_maize.txt | sed 's/?/-/g' > chromosome5_SNP_decreasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome6_SNP_increasing_pos_maize.txt | sed 's/?/-/g' > chromosome6_SNP_decreasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome7_SNP_increasing_pos_maize.txt | sed 's/?/-/g' > chromosome7_SNP_decreasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome8_SNP_increasing_pos_maize.txt | sed 's/?/-/g' > chromosome8_SNP_decreasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome9_SNP_increasing_pos_maize.txt | sed 's/?/-/g' > chromosome9_SNP_decreasing_pos_maize.txt
[cordas@hpc-class BCB546-Spring2022-Ceren]$ sort -r -k3,3 chromosome10_SNP_increasing_pos_maize.txt | sed 's/?/-/g' > chromosome10_SNP_decreasing_pos_maize.txt

In the end, we have 44 files :)

File names for teosinte: 

1. SNP_unknown_positions_teosinte.txt
2. SNP_multiple_positions_teosinte.txt
3. chromosome1_SNP_increasing_pos_teosinte.txt
4. chromosome2_SNP_increasing_pos_teosinte.txt
5. chromosome3_SNP_increasing_pos_teosinte.txt
6. chromosome4_SNP_increasing_pos_teosinte.txt
7. chromosome5_SNP_increasing_pos_teosinte.txt
8. chromosome6_SNP_increasing_pos_teosinte.txt
9. chromosome7_SNP_increasing_pos_teosinte.txt
10. chromosome8_SNP_increasing_pos_teosinte.txt
11. chromosome9_SNP_increasing_pos_teosinte.txt
12. chromosome10_SNP_increasing_pos_teosinte.txt

13. chromosome1_SNP_decreasing_pos_teosinte.txt
14. chromosome2_SNP_decreasing_pos_teosinte.txt 
15. chromosome3_SNP_decreasing_pos_teosinte.txt
16. chromosome4_SNP_decreasing_pos_teosinte.txt
17. chromosome5_SNP_decreasing_pos_teosinte.txt
18. chromosome6_SNP_decreasing_pos_teosinte.txt
19. chromosome7_SNP_decreasing_pos_teosinte.txt
20. chromosome8_SNP_decreasing_pos_teosinte.txt
21. chromosome9_SNP_decreasing_pos_teosinte.txt
22. chromosome10_SNP_decreasing_pos_teosinte.txt

File names for maize:

23. SNP_unknown_positions_maise.txt 
24. SNP_multiple_positions_maise.txt
25. chromosome1_SNP_increasing_pos_maize.txt
26. chromosome2_SNP_increasing_pos_maize.txt
27. chromosome3_SNP_increasing_pos_maize.txt
28. chromosome4_SNP_increasing_pos_maize.txt
29. chromosome5_SNP_increasing_pos_maize.txt
30. chromosome6_SNP_increasing_pos_maize.txt
31. chromosome7_SNP_increasing_pos_maize.txt
32. chromosome8_SNP_increasing_pos_maize.txt
33. chromosome9_SNP_increasing_pos_maize.txt
34. chromosome10_SNP_increasing_pos_maize.txt
35. chromosome1_SNP_decreasing_pos_maize.txt
36. chromosome2_SNP_decreasing_pos_maize.txt
37. chromosome3_SNP_decreasing_pos_maize.txt
38. chromosome4_SNP_decreasing_pos_maize.txt
39. chromosome5_SNP_decreasing_pos_maize.txt
40. chromosome6_SNP_decreasing_pos_maize.txt
41. chromosome7_SNP_decreasing_pos_maize.txt
42. chromosome8_SNP_decreasing_pos_maize.txt
43. chromosome9_SNP_decreasing_pos_maize.txt
44. chromosome10_SNP_decreasing_pos_maize.txt

Make Assignment1FinalFiles and move the final 44 files there:


[cordas@hpc-class BCB546-Spring2022-Ceren]$ mkdir Assignment1Files
[cordas@hpc-class BCB546-Spring2022-Ceren]$ mkdir Assignment1FinalFiles
[cordas@hpc-class BCB546-Spring2022-Ceren]$ mv chromosome* Assignment1FinalFiles/
[cordas@hpc-class BCB546-Spring2022-Ceren]$ mv SNP* Assignment1FinalFiles/

The 44 files are all in Assignment1FinalFiles which is in the Assignment1Files.

git status to to see which files to add and then git commit to commit the files in the local repository.

git add . to add all the files to the given folder.
git status to view the files that are going to be staged to the commit.
git commit -m 'Assignment1Final'
git push to upload it to GitHub and submit it:
git push -u origin master
