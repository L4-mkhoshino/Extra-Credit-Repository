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
This created a mygene folder within the lab5 directory.
```bash
cd ~/labs/lab5-$MYGIT/mygene
```
This takes us into the mygene folder.
```bash
cp ~/labs/lab4-$MYGIT/mygene/mygene.homologs.al.fas ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas
```
This copied the files containing the sequences and alignments from lab 4 into the mygene folder in lab5.
```bash
iqtree -s ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas -bb 1000 -nt 2
```
This command employs IQTree to find the maximum likelihood tree estimate. 
```bash
nw_display ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas.treefile
```
This allows us to view the ASCII graphic produced by IQTree.
```bash
Rscript --vanilla ~/labs/lab5-$MYGIT/plotUnrooted.R  ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas.treefile ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas.treefile.pdf 0.4
```
This reformats the tree produced by IQTree as an unrooted tree. 
```bash
gotree reroot midpoint -i ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.fas.treefile -o ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile
```
This uses gotree to reroot the tree into being a midpoint rooted tree. 
```bash
nw_order -c n ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile  | nw_display -
```
This shows the midpoint rooted tree in ASCII format.
```bash
nw_order -c n ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile | nw_display -w 1000 -b 'opacity:0' -s  >  ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile.svg -
```
This outputs the generated tree as a .svg graphic.
```bash
nw_order -c n ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile | nw_topology - | nw_display -s  -w 1000 > ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.midCl.treefile.svg -
```
This switches the format of the tree to a cladogram. 

# Lab 6
```bash
cd ~/labs/lab6-$MYGIT/mygene
```
This opens the mygene folder.
```bash
ls ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile  
```
This is to make sure that the midpoint rooted tree is within the mygene folder.
```bash
cp ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile
```
This copies the midpoint rooted tree lab5 to lab6.
```bash 
java -jar ~/tools/Notung-3.0-beta/Notung-3.0-beta.jar -s ~/labs/lab5-$MYGIT/species.tre -g ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile --reconcile --speciestag prefix --savepng --events --outputdir ~/labs/lab6-$MYGIT/mygene/
```
This reconciles the gene tree and species tree using notung.
```bash
nw_display ~/labs/lab5-$MYGIT/species.tre
```
This displays the species tree in newick format.
```bash
grep NOTUNG-SPECIES-TREE ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled | sed -e "s/^\[&&NOTUNG-SPECIES-TREE//" -e "s/\]/;/" | nw_display -
```
Using notung, this allows us to view the assigned names of the internal nodes of the tree.
```bash
python2.7 ~/tools/recPhyloXML/python/NOTUNGtoRecPhyloXML.py -g ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled --include.species
```
This converts the format of the reconciled tree into RecPhyloXML format. 
```bash
thirdkind -Iie -D 40 -f ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled.xml -o  ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled.svg
```
This uses thirdkind to view the reconciled tree. 

# Lab 8

```bash
mkdir ~/labs/lab8-$MYGIT/mygene
```
This makes a mygene folder within the lab8 directory.
```bash
cd ~/labs/lab8-$MYGIT/mygene
```
This opens the mygene folder.
```bash
sed 's/*//' ~/labs/lab4-$MYGIT/mygene/mygene.homologs.fas > ~/labs/lab8-$MYGIT/mygene/mygene.homologs.fas
```
Using sed, we copy the raw unaligned sequence to the lab8 folder while also removing the stop codon. 
```bash
wget -O ~/data/Pfam_LE.tar.gz ftp://ftp.ncbi.nih.gov/pub/mmdb/cdd/little_endian/Pfam_LE.tar.gz && tar xfvz ~/data/Pfam_LE.tar.gz  -C ~/data
```
This downloads the pfam database.
```bash
rpsblast -query ~/labs/lab8-$MYGIT/mygene/mygene.homologs.fas -db ~/data/Pfam -out ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out  -outfmt "6 qseqid qlen qstart qend evalue stitle" -evalue .0000000001
```
This command runs the rps blast for the query sequence. This also uses an evalue of 0.0000000001.
```bash
sudo /usr/local/bin/Rscript  --vanilla ~/labs/lab8-$MYGIT/plotTreeAndDomains.r ~/labs/lab5-$MYGIT/mygene/mygene.homologs.al.mid.treefile ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out ~/labs/lab8-$MYGIT/mygene/mygene.tree.rps.pdf
```
This command uses ggtree to plot the phylogeny and drawProteins to plot the pfam domains on the phylogeny. This produces a pdf.
```bash
mlr --inidx --ifs "\t" --opprint  cat ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out | tail -n +2 | less -S
```
This helps to look at the predicted pfam domains without having to push the created pdf from the sudo command to github.
```bash
cut -f 6 ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out | sort | uniq -c
```
This counts how many proteins have more than one annotation.
```bash
cut -f 1 ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out | sort | uniq -c
```
This determines which pfam domain annotation is most found. 
```bash
awk '{a=$4-$3;print $1,'\t',a;}' ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out |  sort  -k2nr
```
This determines which protein has the longest annotated protein domain. 
```bash
sort  -k5rg ~/labs/lab8-$MYGIT/mygene/mygene.rps-blast.out | less -S
```
This shows which protein has the longest annotated protein domain.
