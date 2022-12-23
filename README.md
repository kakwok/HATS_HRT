# Heavy resonance tagging (HRT)
# CMS DAS 2023

The tutorial is heavily based on the jet tagging tools and framework/files.

Produced for the BoostedJet Tagging paper [JME-18-002](http://cms.cern.ch/iCMS/analysisadmin/viewanalysis?id=2101&field=id&value=2101&name=Heavy%20jet%20tagging%20algorithms%20in%2013%20TeV%20data%20(2016%20dataset)) and the corresponding HATS.

DAS exercise in [2022](https://github.com/cms-jet/HATS_HRT/tree/DAS2022)

HATS exercise in [2021](https://github.com/cms-jet/HATS_HRT/tree/HATS2021)

HATS exercise in [2020](https://github.com/gouskos/HATS2020_HRT/blob/master/README.md)

## Setup on LPC
To run on LPC, log in via the command below (**note**: replace `username` with your `FNAL` username!).
```bash
ssh -L localhost:9999:localhost:9999 username@cmslpc-sl7.fnal.gov
```
and setup CMSSW:
```bash
# source /cvmfs/cms.cern.ch/cmsset_default.sh # this should be in your bash profile
mkdir das2023_hrt
cd das2023_hrt
cmsrel CMSSW_11_1_0_pre5
cd CMSSW_11_1_0_pre5/src
git clone https://github.com/IreneZoi/HATS_HRT.git DAS2023HRT -b DAS2023
cmsenv
scram b -j 4
cmsenv
voms-proxy-init -voms cms -valid 192:00
```

Then run the notebook
```bash
jupyter notebook --port 9999 --ip 127.0.0.1 --no-browser
```

## Setup on Vanderbilt
To run on Vanderbilt, login at https://jupyter.accre.vanderbilt.edu/ using your CERN credentials. Once you successfully connect, you should see the following front page

<img src="jupyter-login.png" width="600px" />

The two most important buttons are
  * The `new` button, which lets you open a terminal or start a new Jupyter notebook.
  * The `control panel` button, which lets you shut down your notebook once you're done. It's helpful to do this to free up resources for other users.

#### Upload Grid Certificates - first time only!
We will copy your grid certificates from the LPC cluster, to do this, open the front page (shown above), and click the `New` box at the top right, then the `Terminal` option.

This will open a new tab with a bash terminal. Execute the following commands (following the appropriate prompts) to copy your certificate from the LPC to Jupyter (**note**: replace `username` with your `FNAL` username!)

The following command will prompt you for your FNAL password
```bash
kinit username@FNAL.GOV
rsync -rLv username@cmslpc-sl7.fnal.gov:.globus/ ~/.globus/
chmod 755 ~/.globus
chmod 600 ~/.globus/*
kdestroy
```

#### Initialize Your Proxy at every Login!
If you have a password on your grid certificate, you'll need to remember to execute the following in a terminal *each time you log in to Jupyter*. Similar to the LPC cluster, you will get a new host at each logon, and the new host won't have your old credentials.

Each time you log in, open a terminal and execute:
```bash
voms-proxy-init -voms cms -valid 192:00
```

#### Checkout the code
Open up a terminal and run the following command from your home area:
```bash
mkdir das2023_hrt
cd das2023_hrt
wget https://raw.githubusercontent.com/IreneZoi/HATS_HRT/DAS2023/setup-libraries.ipynb
```


Go back to your Jupyter browser (Home) page and open/run(double-click) the newly downloaded notebook  ([setup-libraries.ipynb](setup-libraries.ipynb) - downloaded just recently - only one cell to run). This will checkout the code and setup your [setup-libraries.ipynb](setup-libraries.ipynb). After running [setup-libraries.ipynb](setup-libraries.ipynb), choose "File... Close and Halt". Then you can continue on to the Exercise section (below).


## Exercise
Run the notebook [taggerComp.py](taggerComp.ipynb)
