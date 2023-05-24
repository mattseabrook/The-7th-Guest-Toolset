2023 refactor of Object Pascal code from 2000-2006 to extract BMP/WAV/AVI from The 7th Guest

**Table-of-Contents**
- [T7GGrvEx](#t7ggrvex)
  - [Build](#build)
    - [Windows \& Mac OS X](#windows--mac-os-x)
    - [Linux](#linux)

## T7GGrvEx

No refactoring was required for this program. 

### Build

#### Windows & Mac OS X

Open `T7GGrvEx.lpi` in Lazarus and press `CTRL`+`F9` to build.

#### Linux

Invoke the Free Pascal Compiler (FPC) from the command-line:

```bash
# Compile
fpc -MObjFPC -Scghi -O1 -g -gl -l -vewnhibq -Fu. -FU. -FE. -oT7GGrvEx T7GGrvEx.pas

# Clean-up
rm -f *.o
```