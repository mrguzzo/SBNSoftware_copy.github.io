# A-frame setup
A-frame mounted with 7 CRT modules (0.96m x 2.73m) placed horizontally and vertically in coincidence for the purposes of module/FEB characterisation using cosmic ray muons. Characterisation tests involve measuring the ADC distribution from SiPMs for MIP muons passing through several modules in coincidence.

[Aframe Run Logs](https://docs.google.com/document/d/1q-qUrJCBgM7efkzxSDImp_Q4yCbnfjuymjgMClU22Zc/edit)

[Aframe Details/photos/timingdelays](https://drive.google.com/drive/folders/1zwgRkR_23Xqraqor5tjULJ4Hr38lZwD5?usp=sharing)

[Testing at DAB Instructions](https://docs.google.com/document/d/1Htx9mYiMXHm6Pj6ZkBWzZnbM_YtGrnx30TityH13OGM/edit?usp=sharing)

![image](https://user-images.githubusercontent.com/74778773/213795237-d53fb05a-e550-49a3-9da4-1f4d4470836f.png)
Figure 1 - Left: Picture of the A-frame setup in the SBN-ND building. Right: Diagram showing the orientation of CRTs with their FEB number (red arrows) and the daisy-chain connection between each FEB (pink arrows) with their respective cable length converted to ns signal delay.

A schematic of the A-frame is shown in figure 1, outlining the daisy-chained cabling between the FEBs connected to the CRTs. The cables connect the T<sub>0</sub>, T<sub>1</sub>, T<sub>in</sub> and T<sub>out</sub> inputs of the FEBs in the following order:

DAQ ----> 92 --2ns--> 73 --10ns--> 75 --6ns--> 76 --8ns--> 72 --6ns--> 71 --8ns--> 82

The T<sub>in</sub> and T<sub>out</sub> daisy-chain loops back from 82 to 92, whereas the T<sub>0</sub> and T<sub>1</sub> chain terminates at 82.
  

# Working directory
- ssh into evb04 with `ssh sbnd-evb04`, then run the `crt_Aframe_launchdaq.sh` script to set up A-frame working directory (`DAQ_DevAreas/DAQ_23Sep2022CRTNoise/srcs/sbndaq/sbn-nd/DAQInterface`) where the `DAQInterface` is run. The crt config file is `crt01.fcl`.

- Raw data is stored in `/daq/scratch/crt_Aframe_data/`. Analysis scripts are in `/home/nfs/sbnd/Aframe`, with each run's analysed root file in the runs folder, all of which analysed using the `analyze_event.fcl` file.

# Side notes for data taking
- Remember to turn on the voltage for the modules before taking the run of data. [These slides](https://sbn-docdb.fnal.gov/cgi-bin/sso/RetrieveFile?docid=24720&filename=SBND_CRT_Power_Supplies_Operation.pdf&version=1) explain how to turn on the voltage. The current setup for A-frame is channel 9.  

- Please fill in the [run logs](https://docs.google.com/document/d/1q-qUrJCBgM7efkzxSDImp_Q4yCbnfjuymjgMClU22Zc/edit) when taking data. 

- Grafana for CRT monitor: 
  - [These slides](https://sbn-docdb.fnal.gov/cgi-bin/sso/RetrieveFile?docid=28335&filename=Grafana%20Tutorial.pdf&version=1) include all details about the CRT monitor grafana page. 
  - Leave a terminal open where you do ```ssh -KL localhost:10089:localhost:10080 sbnd@sbnd-gateway01.fnal.gov 'ssh -KL localhost:10080:localhost:10080 sbnd@sbnd-evb04.fnal.gov'```
  - Then go to localhost:10089/ in your web browser

# Analyse directory 
- ssh into evb04 with `ssh sbnd-evb04`, then run the `ana_launchdaq.sh` script to set up A-frame analysing directory (`DAQ_DevAreas/DAQ_24Sep2022ANA/srcs/`).
sbndaq_artdaq/sbndaq-artdaq/ArtModules/SBND/
- Makes two trees, standard EventAna tree and CRT two-strip-hit tree: CRTHitAna_module.cc
- For SiPM gain measurement analysis: CRTSinglePEAna_module.cc
sbndaq_artdaq/sbndaq-artdaq/ArtModules/Common
- CRT data only, one tree entry per FEB data packet: BernCRTAna_module.cc
- 1730 data only: CAENV1730Dump_module.cc
- many things all together: EventAna_module.cc
fcl scripts to run the above: ~sbnd/ana_crt
analyze_event_hits.fcl: check all fcl params inside, makes CRT two-strip-hit trees
