 # Lab Notebook: Master's Pilot Study    

### Author: Hannah Lachance        

## Overall Description of notebook      

The purpose of this notebook is to keep track of and organize the information that is related to the bioinformatics for the Pilot study conducted during the winter of 2016-2017.


## Date started: 2017-07-24    
## Date end:  ongoing   


### Table of contents for 60 entries (Format is *Page: Date(with year-month-day). Title*)        
* [Page 1: 2017-07-24](#id-section1). VACC server use notes
* [Page 2: 2017-07-26](#id-section2). Setting up remote access to UVM network
* [Page 3: 2017-07-26](#id-section3). Moving programs from PBIO381 server to VACC server
* [Page 4: 2017-07-27](#id-section4). Creating Symlinks for programs
* [Page 5: 2017-02-08](#id-section5). 
* [Page 6: 2017-02-13](#id-section6). 
* [Page 7: 2017-02-15](#id-section7). 
* [Page 8: 2017-02-22](#id-section8). 
* [Page 9: 2017-02-27](#id-section9). 
* [Page 10: 2017-02-28](#id-section10). 
* [Page 11: 2017-03-01](#id-section11). 
* [Page 12: 2017-03-06](#id-section12). 
* [Page 13: 2017-03-06](#id-section13). 
* [Page 14: 2017-03-08](#id-section14). 
* [Page 15: 2017-03-08](#id-section15). 
* [Page 16: 2017-03-20](#id-section16). 
* [Page 17: 2017-03-22](#id-section17). 
* [Page 18: 2017-03-27](#id-section18). 
* [Page 19: 2017-03-29](#id-section19). 
* [Page 20: 2017-04-03](#id-section20). 
* [Page 21: 2017-04-05](#id-section21). 
* [Page 22: 2017-04-05](#id-section22). 
* [Page 23: 2017-04-10](#id-section23).
* [Page 24: 2017-04-12](#id-section24). 
* [Page 25: 2017-04-17](#id-section25). 
* [Page 26: 2017-04-19](#id-section26). 
* [Page 27: 2017-05-03](#id-section27). 
* [Page 28:](#id-section28).
* [Page 29:](#id-section29).
* [Page 30:](#id-section30).
* [Page 31:](#id-section31).
* [Page 32:](#id-section32).
* [Page 33:](#id-section33).
* [Page 34:](#id-section34).
* [Page 35:](#id-section35).
* [Page 36:](#id-section36).
* [Page 37:](#id-section37).
* [Page 38:](#id-section38).
* [Page 39:](#id-section39).
* [Page 40:](#id-section40).
* [Page 41:](#id-section41).
* [Page 42:](#id-section42).
* [Page 43:](#id-section43).
* [Page 44:](#id-section44).
* [Page 45:](#id-section45).
* [Page 46:](#id-section46).
* [Page 47:](#id-section47).
* [Page 48:](#id-section48).
* [Page 49:](#id-section49).
* [Page 50:](#id-section50).
* [Page 51:](#id-section51).
* [Page 52:](#id-section52).
* [Page 53:](#id-section53).
* [Page 54:](#id-section54).
* [Page 55:](#id-section55).
* [Page 56:](#id-section56).
* [Page 57:](#id-section57).
* [Page 58:](#id-section58).
* [Page 59:](#id-section59).
* [Page 60:](#id-section60).   


------

<div id='id-section1'/> 

### Page 1: 2017-07-24. VACC server use notes



When submitting **single jobs** you have to use the following script: (call it: myjob.script)   

```
# This job needs 1 compute node with 1 processor per node.
PBS -l nodes=1:ppn=1
# It should be allowed to run for up to 1 hour.
PBS -l walltime=01:00:00
# Name of job.
PBS -N myjob
# Join STDERR TO STDOUT.  (omit this if you want separate STDOUT AND STDERR)
PBS -j oe   
# Send me mail on job start, job end and if job aborts
PBS -M hlachanc@uvm.edu
PBS -m bea

cd $HOME/myjob
echo "This is myjob running on " `hostname`
myprogram -foo 1 -bar 2 -baz 3

```



Submit the job by running:   

```
qsub myjob.script
```

 

When submitting jobs that require **more memory** (more than 1.5gb) use this script:   

```
# This job is a single process that needs 8gb of physical memory and 9gb of virtual memory
# (it can push 1GB into swap/paging space.)
PBS -l nodes=1:ppn=1,pmem=8gb,pvmem=9gb
# It should be allowed to run for up to 1 hour.
PBS -l walltime=01:00:00
# Name of job.
PBS -N mybigmemjob
# Join STDERR TO STDOUT.  (omit this if you want separate STDOUT AND STDERR)
PBS -j oe   
# Send me mail on job start, job end and if job aborts
PBS -M hlachanc@uvm.edu
PBS -m bea
```



------

<div id='id-section2'/> 

### Page 2: 2017-07-26. Setting up remote access to UVM network 



***Based on notes from meeting with RESNR IT personal Seth O'Brien***   



1. Go to www.uvm.edu/it/network   
2. Click "request VPN Access" in the bottom right column   
3. Agree to the terms and click "Request VPN access"   
4. Access should be granted (via email I believe) within one business day.    


A VPN allows you to access the serves when not connected to a UVM network. (will allow me to work down at the lab or off campus)

   

   



I was granted access within an hour!  Next steps:

1. download the cisco "AnyConnect Secure Mobility Client" by following the steps provided from the link in the email.
2. once eveything is downloaded to use your VPN you:
   1. open the  "AnyConnect Secure Mobility Client" program.
   2. it will list "sslvpn.uvm.edu" and give you the option to click "connect"
   3. once you click "connect" it will ask you to log in (use your UVM net id and password)
   4. then you should be good to go!


------

<div id='id-section3'/> 

### Page 3: 2017-07-26. Moving programs from PBIO381 server to VACC server    



***Based on email instructions form Melissa Pespeni***

Email from Melissa:

1. Login to your home directory on the VACC server, make a programs directory,
2. Open another terminal window and log onto the pbio381 server and cd into the /data/popgen/ directory
3. You can scp whichever or all directories in there that you want with something like:

```
scp -r samtools_1.4 hlachance@vacc.server.edu:/hl/programs/
```

the "-r" tells it to copy a directory

4. Then you can symlink each program to /usr/local/bin - at least that's what we've done on the pbio server to "add things to the PATH" so the computer can find the program when you call.  But I'm not sure if/how this will work on the VACC server.  You may need to ask them or ask Aayudh how he has done it!   


   

   




Steps I took:

1. log onto VACC server (bluemoon-user1.uvm.edu)
2. make sure you are in the home directory then create a directory called "programs"

```
cd ~/
mkdir programs
ll
```

3. Open another terminal window (PUTTY) and log onto "pbio381.uvm.edu" and cd to where the programs are stored:

```
cd /data/popgen
ll
```

4. Open WinSCP and log into both servers (log into one server then open a new tab by clicking the "+" tab and log into the second server)
5. move the programs from the pbio381 directory onto my computer's desktop (temporarily) then go to the tab with the bluemoon-user1 sever and move the programs from my desktop into the "programs" folder. 


------

<div id='id-section4'/> 

### Page 4: 2017-07-27. Creating Symlinks for programs   



I attempted to create symlinks to each program using the following commands.  Each command was run from the programs folder:



symlink to bwa:

```
ln -s ~/programs/bwa/bwa "bwa"
```

 symlink to bowtie:

```
ln -s ~/programs/bowtie/bowtie "bowtie"
```

symlink to fastqc:

```
ln -s ~/programs/fastqc/fastqc "fastqc"
```

symlink to blastp:

```
ln -s ~/programs/ncbi-blast/blastp "blastp"
```

symlink to blastn:

```
ln -s ~/programs/ncbi-blast/blastn "blastn"
```

symlink to blastx:

```
ln -s ~/programs/ncbi-blast/blastx "blastx"
```



symlink to samtools:

```
ln -s ~/programs/samtools-1.4/samtools "samtools"
```

symlink to Trimmomatic:

```
ln -s ~/programs/Trimmomatic-0.33/trimmomatic-0.33.jar "trimmomatic"
```

symlink to trinity:

```
ln -s ~/programs/trinityrnaseq-Trinity-v2.4.0/Trinity "trinity"
```



Oops: actually I ran the commands when I was in "Trimmomatic-0.33" so now I have to go delete them and re-run the commands while in a new directory which I will create and call "symlinks":



Make Directory and enter in the folder:

```
mkdir symlinks
```

Deleted symlinks in "Trimmomatic-0.33" using **WinSCP**



Re-run symlink commands while in "symlinks" folder:

```
ln -s ~/programs/bwa/bwa "bwa"
ln -s ~/programs/bowtie/bowtie "bowtie"
ln -s ~/programs/fastqc/fastqc "fastqc"
ln -s ~/programs/ncbi-blast/blastp "blastp"
ln -s ~/programs/ncbi-blast/blastn "blastn"
ln -s ~/programs/ncbi-blast/blastx "blastx"
ln -s ~/programs/samtools-1.4/samtools "samtools"
ln -s ~/programs/Trimmomatic-0.33/trimmomatic-0.33.jar "trimmomatic"
ln -s ~/programs/trinityrnaseq-Trinity-v2.4.0/Trinity "trinity"
```



------

<div id='id-section5'/> 

### Page 5: 2017-07-28. Make programs executable  



The program files were not showing up green which means they were not executable.  Following Melissa's suggestion I used the following commands on each program to make then executable.



```
cd ~/programs/bwa
chmod u+x bwa
ll
cd ~/programs/bowtie
chmod u+x bowtie
ll
cd ~/programs/fastqc
chmod u+x fastqc
ll
cd ~/programs/ncbi-blast
chmod u+x blastp
ll
cd ~/programs/ncbi-blast
chmod u+x blastn
ll
cd ~/programs/ncbi-blast
chmod u+x blastx
ll
cd ~/programs/samtools-1.4
chmod u+x samtools
ll
cd ~/programs/Trimmomatic-0.33
chmod u+x trimmomatic-0.33.jar
ll
cd ~/programs/trinityrnaseq-Trinity-v2.4.0
chmod u+x Trinity
ll
```

They all turned green after the above commands were run.  Still hard to tell if they will work.  When I typed just the program name no list of commands popped up like I was told they would...

------

<div id='id-section6'/> 

### Page 6:  

------

<div id='id-section7'/> 

### Page 7: 

------

<div id='id-section8'/> 

### Page 8: 

------

<div id='id-section9'/> 

### Page 9: 

------

<div id='id-section10'/> 

### Page 10:   
------

<div id='id-section11'/> 

### Page 11:   

------

<div id='id-section12'/> 

### Page 12:   

------

<div id='id-section13'/> 

### Page 13:   

------


<div id='id-section14'/> 

### Page 14:   

------

<div id='id-section15'/> 

### Page 15:   

------

<div id='id-section16'/> 

### Page 16:   

------

<div id='id-section17'/> 

### Page 17:   

------

<div id='id-section18'/> 

### Page 18:    

------

<div id='id-section19'/> 

### Page 19:   

------

<div id='id-section20'/> 

### Page 20:   

------

<div id='id-section21'/> 

### Page 21:   

------

<div id='id-section22'/> 

### Page 22:      

------

<div id='id-section23'/> 

### Page 23:       

------

<div id='id-section24'/> 

### Page 24:   

------

<div id='id-section25'/> 

### Page 25:   

------

<div id='id-section26'/> 

### Page 26:   

------

<div id='id-section27'/> 

### Page 27:    

------

<div id='id-section28'/> 

### Page 28:  

------

<div id='id-section29'/> 

### Page 29:  

------

<div id='id-section30'/> 

### Page 30:  

------

<div id='id-section31'/> 

### Page 31:  

------

<div id='id-section32'/> 

### Page 32:  

------

<div id='id-section33'/> 

### Page 33:  

------

<div id='id-section34'/> 

### Page 34:  

------

<div id='id-section35'/> 

### Page 35:  

------

<div id='id-section36'/> 

### Page 36:  

------

<div id='id-section37'/> 

### Page 37:  

------

<div id='id-section38'/> 

### Page 38:  

------

<div id='id-section39'/> 

### Page 39:  

------

<div id='id-section40'/> 

### Page 40:  

------

<div id='id-section41'/> 

### Page 41:  

------

<div id='id-section42'/> 

### Page 42:  

------

<div id='id-section43'/> 

### Page 43:  

------

<div id='id-section44'/> 

### Page 44:  

------

<div id='id-section45'/> 

### Page 45:  

------

<div id='id-section46'/> 

### Page 46:  

------

<div id='id-section47'/> 

### Page 47:  

------

<div id='id-section48'/> 

### Page 48:  

------

<div id='id-section49'/> 

### Page 49:  

------

<div id='id-section50'/> 

### Page 50:  

------

<div id='id-section51'/> 

### Page 51:  

------

<div id='id-section52'/> 

### Page 52:  

------

<div id='id-section53'/> 

### Page 53:  

------

<div id='id-section54'/> 

### Page 54:  

------

<div id='id-section55'/> 

### Page 55:  

------

<div id='id-section56'/> 

### Page 56:  

------

<div id='id-section57'/> 

### Page 57:  

------

<div id='id-section58'/> 

### Page 58:  

------

<div id='id-section59'/> 

### Page 59:  

------

<div id='id-section60'/> 

### Page 60:  

------