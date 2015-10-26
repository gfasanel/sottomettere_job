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

###M machines

http://mon.iihe.ac.be/trac/t2b/wiki/localSubmission

```
mkdir directsubmissiontest
cd directsubmissiontest/
emacs script.sh&
pwd=$PWD
source $VO_CMS_SW_DIR/cmsset_default.sh
cd /localgrid/<USER NAME>/path/to/CMSSW_4_1_4/src/
eval `scram runtime -sh`              
cd $pwd

mkdir /localgrid/$USER/directsubmissiontest
qsub -q localgrid@cream02 -o script.stdout -e script.stderr script.sh
qstat -u $USER localgrid@cream02
http://mon.iihe.ac.be/ganglia/addons/job_monarch/?c=Servers

#Quando i job sono finiti
emacs /localgrid/$USER/directsubmissiontest/script.stdout
emacs /localgrid/$USER/directsubmissiontest/script.stderr
ls /localgrid/$USER/directsubmissiontest/
```


