# plumed2_TALOS_maincode
Maincode of TALOS at PLUMED 2.5.1

How to install:
1. Install DyNet library (https://dynet.readthedocs.io) and set DyNet at environment variable
2. Copy and replace all the files to the directory of PLUMED
3. Execute “autoconf” command at the root directory of PLUMED
4. Execute “./configure --enable-modules=all” at the root directory of PLUMED
5. If DyNet link success, you will see: “checking dynet with -ldynet... yes”
6. Recompile PLUMED

An example of input file:

MOLINFO STRUCTURE=./alad.pdb
WHOLEMOLECULES STRIDE=1 ENTITY0=1-22

phi: TORSION ATOMS=@phi-2
psi: TORSION ATOMS=@psi-2

bff: BF_FOURIER MINIMUM=-pi MAXIMUM=+pi ORDER=8
tdu: TD_UNIFORM

VES_LINEAR_EXPANSION ...
 LABEL=ves
 ARG=phi,psi
 BASIS_FUNCTIONS=bff,bff
 TEMP=300
 GRID_BINS=180,180
 TARGET_DISTRIBUTION=tdu
 BIAS_FILE=bias
 FES_FILE=fes
... VES_LINEAR_EXPANSION

OPT_TALOS ...
 BIAS=ves
 ARG=phi,psi
 GRID_MIN=-pi,-pi
 GRID_MAX=pi,pi
 GRID_BINS=60,60
 UPDATE_STEPS=1000
 EPOCH_NUM=4
 HIDDEN_NUMBER=3
 HIDDEN_LAYER=16
 HIDDEN_ACTIVE=RELU
 CLIP_RANGE=-0.01,0.01
 LABEL=opt
 COEFFS_FILE=coeffs.data
 FES_OUTPUT=100
 BIAS_OUTPUT=100
 COEFFS_OUTPUT=100
... OPT_TALOS

PRINT ...
  ARG=phi,psi
  FILE=colvar.info.data
  STRIDE=100
... PRINT

PRINT ...
  ARG=ves.*,opt.*
  FILE=colvar.bias.data
  STRIDE=100
... PRINT

