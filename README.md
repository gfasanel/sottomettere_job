# sottomettere_job

Il cuore di tutto e' in una istruzione tipo questa

````
bsub -q 1nh -eo err.dat -oo out.dat -J "nome job" "cd $PWD; eval \`scramv1 runtime -sh\`; uname -a; echo \$CMSSW_VERSION;  ls"
```

Se hai bisogno puoi decidere di sottomettere su macchine che abbiano una certa RAM minima 

```
bsub -R "rusage[mem=10000]
```
Puoi anche mettere una istruzione tipo "quando i job sono finiti fai questa cosa"

```
while [ "`bjobs | grep JOBID | wc -l`" != "0" ]; do /bin/sleep 2m; done
istruzione a job finiti
```
