```
The workflow given below has only been verified for builds where target=riscv32-unknown-elf.
```

# 1. Clone the crosstool-ng repository: 
```
git clone https://github.com/crosstool-ng/crosstool-ng
cd crosstool-ng
```

# 2. Depedency for linux				
```
sudo apt install autoconf automake bison build-essential  gawk gcc gpp g++ gdb flex bzip2 unzip help2man lzip make libtool-bin ncurses5-dev python3-dev python3-distutils cmake-curses-gui
```

# 3. Additional Depedency for windows  
```
sudo apt install gcc-mingw-w64 g++-mingw-w64
```

#4. compile
```
./bootstrap
./configure
./make
sudo make install
```
Note: (Do not run make install with enable-local option added in config), Add ct-ng to path or alias it in .bashrc if you are installing local path

#5. Using with previous sample config file
```
mkdir build
cd build
cp ../samples/riscv64-rdno-elf/crosstool.config ./config
ct-ng upgradeconfig
```

#6. Using ct-ng gui
```
ct-ng menuconfig
```


Note: 
* use [ct-ng list-options] for  accessing  viewing all optins.
* use [ct-ng <option>} to set the option needed. ({riscv(64/32)-(unknown/multilib)-elf} in our case)

#7. Download the RISCV GNU Toolchain from github on your machine.

#8.Configuring ct-ng  using GUI.
	
```
	Toolchain Options:
	//(for building linux-riscv cross compiler)
		Type: Cross
		Tuple: x86_64-pc-linux-gnu  ( Build Machine=64 bit x-86 linux )
		
	//(for building windows-riscv cross compiler)
		Type: Canadian
		Build System Tuple:x86_64-pc-linux-gnu 
		Host  System Tuple:x86_64-w64-mingw32
	
	Operating System:
		Target OS:bare-metal (default)
		
	Binary Utilities:
		Source of binutils:Custom Location
		Custom source Location:(path of riscv-gnu-toolchain)/binutils
		binutils patches of origin: Local only
		
	C-library:
		Source of newlib:Custom Location
		Custom source Location:(path of riscv-gnu-toolchain)/newlib
		newlib patches of origin :Local only
		
	C compiler:
		Source of gcc: Custom Location
		Custom source Location:(path of riscv-gnu-toolchain)/gcc
		gcc patches of origin:Local only
		
	Debug facilities:
	//Choose gdb option in the menu first
		Source of gdb: Custom Location
		Custom source Location:(path of riscv-gnu-toolchain)/gdb
		gdb patches of origin:Local only
```
	
	
# 11. run {ct-ng build}



/*
 ->For adding custom instructions to the compiler modify binutils by following the workflow for adding custom instructions 
 ->NOTE:LD_LIBRARY_PATH should'nt be set for ct-ng builds.
 ->gdb is working only for linux cross-compilers.Some errors are occuring while unning windows-riscv-gdb.
*/
