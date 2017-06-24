# NaiveBcell
# Data from GSE71702
# Data stored in Fudge file

## Extract only chrposition and methylation ratio
awk '{print $1,$6} masterNB1.txt > A.txt
awk '{print $1,$6} masterNB2.txt > B.txt
awk '{print $1,$6} masterNB3.txt > C.txt
awk '{print $1,$6} masterNB4.txt > D.txt

## Sort 
sort -n A.txt 
sort -n B.txt 
sort -n C.txt 
sort -n D.txt 

## Join
join C.txt D.txt > CD.txt
join CD.txt B.txt > BCD.txt
join BCD.txt A.txt > ABCD.txt

## Unmethylated group (meth < 25)
awk '{if ($2 < 25 && $3 < 25 && $4 < 25 && $5 < 25) print $1,$2,$3,$4,$5}' ABCD.txt > UM.txt

## Methylated group (meth > 75)
awk '{if ($2 > 75 && $3 > 75 && $4 > 75 && $5 > 75) print $1,$2,$3,$4,$5}' ABCD.txt > M.txt

## Partially methylated group ( 25 < meth < 75)
awk '{if ($2 >= 25 && $2 <= 75 && $3 >= 25 && $3 <= 75 &&$4 >= 25 && $4 <= 75 && $5 >= 25 && $5 <= 75) print $1,$2,$3,$4,$5}' ABCD.txt > tryPM.txt
