# Extra-Credit-Repository
**Maia Hoshino BIO 312 Extra Credit**
# Lab 4
```bash
mkdir ~/labs/lab4-$MYGIT/mygene
```
This command made a folder for mygene within the lab4 directory.
```bash
cd ~/labs/lab4-$MYGIT/mygene
```
This command takes us into the mygene folder within the lab4 directory.
```bash
seqkit grep --pattern-file ~/labs/lab3-$MYGIT/mygene/mygene.blastp.detail.filtered.out ~/labs/lab3-$MYGIT/allprotein.fas > ~/labs/lab4-$MYGIT/mygene/mygene.homologs.fas
```
Using seqkit, the sequences of mygene from the BLAST output file were obtained and put into the lab4 directory within the mygene folder. 
```bash
muscle -in ~/labs/lab4-$MYGIT/mygene/mygene.homologs.fas -out ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.fas
```
This command uses muscle to create a multiple sequence alignment using the sequences from the BLAST output file. 
```bash
alv -kli  ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.fas | less -RS
```
This allows us to view the alignment using alv. 
```bash
alv -ki -w 100 ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.fas | aha > ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.html
a2ps -r --columns=1 ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.html -o ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.ps
ps2pdf ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.ps ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.pdf
```
This set of commands allowed us to convert the multiple sequence alignment to a pdf, using alv to view it. 
```bash
alignbuddy  -al  ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.fas
```
This calculated the width of the alignment.
```bash
alignbuddy -trm all  ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.fas | alignbuddy  -al
```
This calculated the width of the alignments after removing gaps.
```bash
alignbuddy -dinv 'ambig' ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.fas | alignbuddy  -al
```
This outputs the width of the alignment after removing completely conserved areas.
```bash
t_coffee -other_pg seq_reformat -in ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.fas -output sim
```
This uses t_coffee to find the average percent identity.
```bash
alignbuddy -pi ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.fas | awk ' (NR>2)  { for (i=2;i<=NF  ;i++){ sum+=$i;num++} }
     END{ print(100*sum/num) } '
```
This uses alignbuddy to calculate the average percent identity. 

# Lab 5
```bash
mkdir ~/labs/lab5-$MYGIT/mygene
```

```bash
cd ~/labs/lab5-$MYGIT/mygene
```

```bash
cp ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.fas ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas
```

```bash
iqtree -s ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas -bb 1000 -nt 2
```

```bash
nw_display ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas.treefile
```

```bash
Rscript --vanilla ~/labs/lab5-$MYGIT/plotUnrooted.R  ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas.treefile ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas.treefile.pdf 0.4
```

```bash
gotree reroot midpoint -i ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas.treefile -o ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile
```

```bash
nw_order -c n ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile  | nw_display -
```

```bash
nw_order -c n ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile | nw_display -w 1000 -b 'opacity:0' -s  >  ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile.svg -
```

```bash
nw_order -c n ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile | nw_topology - | nw_display -s  -w 1000 > ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.midCl.treefile.svg -
```

# Lab 6

```bash 
java -jar ~/tools/Notung-3.0-beta/Notung-3.0-beta.jar -s ~/labs/lab5-$MYGIT/species.tre -g ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile --reconcile --speciestag prefix --savepng --events --outputdir ~/labs/lab6-$MYGIT/mygene/
```

```bash
grep NOTUNG-SPECIES-TREE ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled | sed -e "s/^\[&&NOTUNG-SPECIES-TREE//" -e "s/\]/;/" | nw_display -
```

```bash
python2.7 ~/tools/recPhyloXML/python/NOTUNGtoRecPhyloXML.py -g ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled --include.species
```

```bash
thirdkind -Iie -D 40 -f ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled.xml -o  ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled.svg
```

# Lab 8

```bash
mkdir ~/labs/lab8-$MYGIT/mygene
```

```bash
cd ~/labs/lab8-$MYGIT/mygene
```

```bash
sed 's/*//' ~/labs/lab4-$MYGIT/mygene/mygene.homologs.fas > ~/labs/lab8-$MYGIT/mygene/mygene.homologs.fas
```

```bash
rpsblast -query ~/labs/lab8-$MYGIT/mygene/mygene.homologs.fas -db ~/data/Pfam -out ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out  -outfmt "6 qseqid qlen qstart qend evalue stitle" -evalue .0000000001
```

```bash
mlr --inidx --ifs "\t" --opprint  cat ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out | tail -n +2 | less -S
```

```bash
cut -f 6 ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out | sort | uniq -c
```

```bash
cut -f 1 ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out | sort | uniq -c
```

```bash
awk '{a=$4-$3;print $1,'\t',a;}' ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out |  sort  -k2nr
```

```bash
sort  -k5rg ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out | less -S
```

```bash
sudo /usr/local/bin/Rscript  --vanilla ~/labs/lab8-$MYGIT/plotTreeAndDomains.r ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out ~/labs/lab8-$MYGIT/mygene/mygene.tree.rps.pdf
```
