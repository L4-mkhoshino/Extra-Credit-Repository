# Extra-Credit-Repository
**Maia Hoshino BIO 312 Extra Credit**
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
