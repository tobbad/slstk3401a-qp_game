# slstk3401a-qp_game
This is the working project with quantum Leaps qpc frame work which will be used in the focus group.

# Building

Please checkout the [source](https://github.com/tobbad/slstk3401a-qp_game) with:

```bash 
git clone --recurse-submodules https://github.com/tobbad/slstk3401a-qp_game.git
```

Before building the binary the generated code must be generated. Load the `game.qm` in the QM (QP Modeler) Version >= 4.5. After successful loading of the file generate the needed source by pressing the related button, pressing F7 or choosing from the menu `Tools->Generate Code`.

After these steps choose the binary to generate (either `qv/gnu` or `qk/gnu`) and adapt the `GNU_ARM` variable in the head of the `Makefile` to point to the location of your Gnu Tool chain downloaded from [here](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads) and installed on your computer. The setting in the Makefile assumes that you are working on a Linux PC and installed the toolchain at `/opt/gnu-arm-none-eabi/` and created a logical link from the install folder to `current`. For example by entering the command:

```bash
sudo ln -s /opt/gnu-arm-none-eabi/gcc-arm-none-eabi-8-2019-q3-update /opt/gnu-arm-none-eabi/current
```
  
