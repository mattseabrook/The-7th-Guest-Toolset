2023 refactor of Object Pascal code from 2000-2006 to extract BMP/WAV/AVI from The 7th Guest

**Table-of-Contents**
- [T7GGrvEx](#t7ggrvex)
  - [Build](#build)
    - [Windows \& Mac OS X](#windows--mac-os-x)
    - [Linux](#linux)
  - [Usage](#usage)
- [VDXExt](#vdxext)
  - [Build](#build-1)
    - [Windows](#windows)
    - [Linux \& Mac OS X](#linux--mac-os-x)
  - [Usage](#usage-1)
  - [2023 Modifications](#2023-modifications)
    - [Error: Incompatible types: got "Pointer" expected "TBitmap"](#error-incompatible-types-got-pointer-expected-tbitmap)
    - [External Function Declarations](#external-function-declarations)
    - [Error: Incompatible type for arg no. 5: Got "TBuffer", expected "Pointer"](#error-incompatible-type-for-arg-no-5-got-tbuffer-expected-pointer)
    - [LCL, LCLBase, and Interfaces](#lcl-lclbase-and-interfaces)

# T7GGrvEx

No refactoring was required for this program. 

## Build

### Windows & Mac OS X

Open `T7GGrvEx.lpi` in Lazarus and press `CTRL`+`F9` to build.

### Linux

Invoke the Free Pascal Compiler (FPC) from the command-line:

```bash
# Compile
fpc -MObjFPC -Scghi -O1 -g -gl -l -vewnhibq -Fu. -FU. -FE. -oT7GGrvEx T7GGrvEx.pas

# Clean-up
rm -f *.o
```

## Usage

x

# VDXExt

Check out the section below for a full list of modifications made to the original source code.

## Build

### Windows

Open `VDXExt.lpi` in Lazarus and press `CTRL`+`F9` to build.

### Linux & Mac OS X

`avifil32.dll` is a Windows DLL that is required to compile the program. It is not available on Linux or Mac OS X.

## Usage

x

## 2023 Modifications

### Error: Incompatible types: got "Pointer" expected "TBitmap"

This error message indicates that the variable `Bitmaps[i]` is a pointer, but `ExtBitmap` is expecting a `TBitmap`.

`ExtBitmap := Bitmaps[i];` was changed to `ExtBitmap := TBitmap(Bitmaps[i]);` twice in `AviWriter.pas` on line 350 and 460.

### External Function Declarations

Modern compilers like Free Pascal Compiler (FPC), used in the Lazarus IDE, have introduced new standards and practices to improve code safety, readability, and maintainability. This includes stricter typing and syntax rules that can lead to issues when trying to compile older Delphi code that was written under a different set of standards.

The original code used an older syntax for declaring external functions that is no longer accepted by modern Pascal compilers. The new syntax requires you to provide the name of the DLL and the name of the function in the DLL in the external function declaration. 

The following changes were made to `AviWriter.pas` (original commented out):

```pascal
  {
  function AVIFileOpen; external 'avifil32.dll' name 'AVIFileOpenA';
  function AVIFileCreateStream; external 'avifil32.dll' name 'AVIFileCreateStreamA';
  function AVIStreamSetFormat; external 'avifil32.dll' name 'AVIStreamSetFormat';
  function AVIStreamReadFormat; external 'avifil32.dll' name 'AVIStreamReadFormat';
  function AVIStreamWrite; external 'avifil32.dll' name 'AVIStreamWrite';
  function AVIStreamRelease; external 'avifil32.dll' name 'AVIStreamRelease';
  function AVIFileRelease; external 'avifil32.dll' name 'AVIFileRelease';
  function AVIFileGetStream; external 'avifil32.dll' name 'AVIFileGetStream';
  function CreateEditableStream; external 'avifil32.dll' name 'CreateEditableStream';
  function AVISaveV; external 'avifil32.dll' name 'AVISaveV';
  }

  function AVIFileOpen(var ppfile: PAVIFile; szFile: PChar; uMode: UINT; lpHandler: pointer): HResult; stdcall; external 'avifil32.dll' name 'AVIFileOpenA';
  function AVIFileCreateStream(pfile: PAVIFile; var ppavi: PAVISTREAM; var psi: TAVIStreamInfo): HResult; stdcall; external 'avifil32.dll' name 'AVIFileCreateStreamA';
  function AVIStreamSetFormat(pavi: PAVIStream; lPos: LONG; lpFormat: pointer; cbFormat: LONG): HResult; stdcall; external 'avifil32.dll' name 'AVIStreamSetFormat';
  function AVIStreamReadFormat(pavi: PAVIStream; lPos: LONG; lpFormat: pointer; var cbFormat: LONG): HResult; stdcall; external 'avifil32.dll' name 'AVIStreamReadFormat';
  function AVIStreamWrite(pavi: PAVIStream; lStart, lSamples: LONG; lpBuffer: pointer; cbBuffer: LONG; dwFlags: DWORD; var plSampWritten: LONG; var plBytesWritten: LONG): HResult; stdcall; external 'avifil32.dll' name 'AVIStreamWrite';
  function AVIStreamRelease(pavi: PAVISTREAM): ULONG; stdcall; external 'avifil32.dll' name 'AVIStreamRelease';
  function AVIFileRelease(pfile: PAVIFile): ULONG; stdcall; external 'avifil32.dll' name 'AVIFileRelease';
  function AVIFileGetStream(pfile: PAVIFile; var ppavi: PAVISTREAM; fccType: DWORD; lParam: LONG): HResult; stdcall; external 'avifil32.dll' name 'AVIFileGetStream';
  function CreateEditableStream(var ppsEditable: PAVISTREAM; psSource: PAVISTREAM): HResult; stdcall; external 'avifil32.dll' name 'CreateEditableStream';
  function AVISaveV(szFile: PChar; pclsidHandler: PCLSID; lpfnCallback: TAVISaveCallback; nStreams: integer; pavi: APAVISTREAM; lpOptions: APAVICompressOptions): HResult; stdcall; external 'avifil32.dll' name 'AVISaveV';
  ```

  ### Error: Incompatible type for arg no. 5: Got "TBuffer", expected "Pointer"

  The procedure `Dump8BitBMP` seems to be expecting a Pointer type as its fifth argument, but `OutBuf` which is of type `TBuffer` is being passed instead.

If `TBuffer` is a dynamic array, you can pass a pointer to its first element to the Dump8BitBMP procedure:

  ```pascal
  {
  Dump8BitBMP(Prefix(VDXName) + '#' + IntToStrL(VidFrames - 1, 4) + '.bmp',
    BMPHeader.Width, BMPHeader.Height, Palette3, OutBuf);
  }
  Dump8BitBMP(Prefix(VDXName) + '#' + IntToStrL(VidFrames - 1, 4) + '.bmp',
    BMPHeader.Width, BMPHeader.Height, Palette3, @OutBuf[0]);
```

### LCL, LCLBase, and Interfaces

- The `uses` clause was updated to include `Interfaces`
- `LCL` and `LCLBase` were added to the Lazarus project file dependencies