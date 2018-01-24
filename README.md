
### How to run the W-tagging scalefactor code ###
#########################################

## installation instructions
Setup CMSSW and get nanoAOD packages
```
cmsrel CMSSW_9_4_2
cd CMSSW_9_4_2/src
cmsenv
git checkout -b nanoAOD cms-nanoAOD/master
git clone https://github.com/cms-nanoAOD/nanoAOD-tools.git PhysicsTools/NanoAODTools
scram build
```

### getting the code
First fork your own version of the repository at https://github.com/BoostedScalefactors/WTopScalefactorProducer
```
export GITUSER=`git config user.github`
echo "Your github username has been set to \"$GITUSER\""
git clone -b nanoOAD git@github.com:${GITUSER}/WTopScalefactorProducer.git
cd WTopScalefactorProducer
git remote add originalRemote git@github.com:BoostedScalefactors/WTopScalefactorProducer.git
```
### Producing samples

See README in subdirectory skim_nanoAOD/
```
cd skim_nanoAOD/
python process_nanoAOD.py
```

### running scalefactor code

```
python Automatic_Setup.py #To compile
python runSF.py -b   #To run
```

The basic script to be run is 

```
python runSF.py
```
It takes as input .root files containing a TTree with a branch for the mass distribution you want to calculate a scale factor for. This branch can contain events after full selection is applied, or new selections can be implemented on the fly in wtagSFfits.py. In addition to a data and the separate background MC files, you need one file called "*pseudodata* which contains all MC added together (with their appropriate weights, using ROOT hadd).

   
   General Options:
```
    -b : To run without X11 windows
    -c : channel you are using(electron,muon or electron+muon added together)
    --HP : HP working point
    --LP : LP working point
    --fitTT : Only do fits to truth matched tt MC
    --fitMC : Only do fits to MC (test fit functions)
    --sample : name of TT MC eg --sample "herwig"
    --doBinned : to do binned simultaneous fit (default is unbinned)
    --76X : Use files with postfix "_76X" (change to postfix of your choice if running on several different samples)
    --useDDT : Uses DDT tagger instead of pruning+softdrop (ops! Requires softdrop variables)
    --usePuppiSD : Uses PUPPI + softdrop and PUPPI n-subjettiness
```
