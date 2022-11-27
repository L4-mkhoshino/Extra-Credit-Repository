# Extra-Credit-Repository
**Maia Hoshino BIO 312 Extra Credit**
# Lab 6

``` java -jar ~/tools/Notung-3.0-beta/Notung-3.0-beta.jar -s ~/labs/lab5-$MYGIT/species.tre -g ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile --reconcile --speciestag prefix --savepng --events --outputdir ~/labs/lab6-$MYGIT/mygene/ 
```

``` grep NOTUNG-SPECIES-TREE ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled | sed -e "s/^\[&&NOTUNG-SPECIES-TREE//" -e "s/\]/;/" | nw_display - ```

python2.7 ~/tools/recPhyloXML/python/NOTUNGtoRecPhyloXML.py -g ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled --include.species
thirdkind -Iie -D 40 -f ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled.xml -o  ~/labs/lab6-$MYGIT/mygene/mygene.homologs.al.mid.treefile.reconciled.svg
