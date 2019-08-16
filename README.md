# slstk3401a-qp_game
This is the working project with quantum Leaps qpc frame work which will be used in the focus group.

# Install Tools
Please proceed as described on the [GNU MCU Eclipse](https://gnu-mcu-eclipse.github.io/install/) page described. After these steps you will have the Gnu ARM Toolchain the Eclipse CDT with MCU plugins, SEGGER debug tools and the OCD debugger installed on zour computer.

For the npm installation I propose not to install the binary packages in the Roaming profile. Therfore change the setting with the [commands](https://www.davidyardy.com/blog/change-default-global-installation-directory-for-nodejs-on-windows/):

```bash
npm config set prefix c:\\npm
npm config set cache c:\\npm-cache 
```
Further change the location of the xPack install to be not in the ROAMING profile by setting the environment Variable ```XPACKS_REPO_FOLDER```.

Further intall the Quantum-Leaps [qm (Modelling tool)](https://github.com/QuantumLeaps/qm/releases/download/v4.5.1/qm_4.5.1-win32.exe) on your PC.

# Building

Please checkout the [source](https://github.com/tobbad/slstk3401a-qp_game) with:

```bash 
git clone --recurse-submodules https://github.com/tobbad/slstk3401a-qp_game.git
```

Before building the binary the generated code must be generated. Load the `game.qm` in the QM (QP Modeler) Version >= 4.5. After successful loading of the file generate the needed source by pressing the related button, pressing F7 or choosing from the menu `Tools->Generate Code`.

## On Linux with command line 

After these steps choose the binary to generate (either `qv/gnu` or `qk/gnu`) and adapt the `GNU_ARM` variable in the head of the `Makefile` to point to the location of your installed Gnu Tool chain which is either downloaded from [here](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads) or earlier installed with xpm. The setting in the Makefile assumes that you are working on a Linux PC and installed the toolchain at `/opt/gnu-arm-none-eabi/` and created a logical link from the install folder to `current`. For example by entering the command:

```bash
sudo ln -s /opt/gnu-arm-none-eabi/gcc-arm-none-eabi-8-2019-q3-update /opt/gnu-arm-none-eabi/current
```

## Import the project into the Eclipse Workspace
This should be done by right clicking on the "Project Explorere" (left pane in Eclipse) and then "Import". Chose "Existing Projects into Workspace" and then "Next". Browse to the root of the Project and then the project should be selected. There are two Build Configuration (Right click on the project in the Project explorere) which can be activated. Please chose the qk project which uses the preemptive Kernel. This can be accomplished by right click on the Project "Build Configuration"->"Set Active"->"qk". With this configuration the Makefile in the qk/gnu folder is called. If you'd like to compile the vanilla kernel based project choose the qv Build configuration. To successful compile the code you have to adapt the Makefile in the related project.


## On Linux with eclipse
Import the project into the workspace. and adapte the `GNU_ARM` path in the make file to match the location of your GNU ARM Toolchain. Press CTRL-B to start the build.

## On Windows with eclipse
Set `XPACKS_REPO_FOLDER` to match the location where you installed the xPacks with xpm. Modify the `GNU_ARM` variable in the Makefile to match the location of the Gnu tool chain. Import the project into the workspace and adapte the `GNU_ARM` path in the Makefiles to match the location of your GNU ARM Toolchain. Eg:

```bash
GNU_ARM := ${XPACKS_REPO_FOLDER}/@gnu-mcu-eclipse/arm-none-eabi-gcc/8.2.1-1.7.1/.content/
```
Press CTRL-B to start the build.

# Debug
Connect the development kit by USB to the PC. Start Debugging by `Run->Debug Configuiration` and then chossing `GDB SEGGER J-Link Debugging`. On the Main Tab choose the elf file to debug (either the qk or the qv variant, maybe press `Search Project`). in The Debugger Tab enter `EFM32PG1B200F256GM48` in the `Device name` field. Maybe you have to prepend the text in the `Executable name` filed with the location of your GNU Toolchain (eg. `${XPACKS_REPO_FOLDER}/@gnu-mcu-eclipse/arm-none-eabi-gcc/8.2.1-1.7.1/.content/` YMMV). Press Apply and then Debug.

# Final Remarks
You may ask yourself why not using the Silicon Lab Tool Symplicity Studio. I have no direct opposition against this tool. However setting up Eclipse the way described here you have an installation which you can as well use to compile software for many different MCUs of different vendors. If you use a Vendor distributed variant of Eclipse (Simplicity Studio, Code Composer, TrueStudio ...) you may have more vendor specific feature but loose the flexibility in choosing an MCU. (Vendor Lockin).
