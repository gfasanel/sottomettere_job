# sottomettere_job

````
bsub -q 1nh -eo err.dat -oo out.dat -J "nome job" "cd $PWD; eval \`scramv1 runtime -sh\`; uname -a; echo \$CMSSW_VERSION;  ls"
```

Il cuore di tutto e' in una istruzione tipo questa
