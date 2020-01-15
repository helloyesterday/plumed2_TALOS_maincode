# plumed2_TALOS_maincode
Maincode of TALOS at PLUMED 2.5.1

How to install:
1. Install DyNet library (https://dynet.readthedocs.io) and set DyNet at environment variable
2. Copy and replace all the files to the directory of PLUMED
3. Execute “autoconf” command at the root directory of PLUMED
4. Execute “./configure --enable-modules=all” at the root directory of PLUMED
5. If DyNet link success, you will see: “checking dynet with -ldynet... yes”
6. Recompile PLUMED

