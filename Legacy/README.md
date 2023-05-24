# Utilities for The 7th Guest

Copyright (C) 2000-2006 Deniz Oezmen (http://oezmen.eu/)

All trademarks and copyrights mentioned implicitly or explicitly in this file or the software described below are property of their respective owners.

## T7GGrvEx

Extracts files from RL/GJD archives.

```
Usage:  T7GGrvEx <RLFile> <GJDFile>

        RLFile          Specifies the RL file to be processed.
        GJDFile         Specifies the matching GJD file.
```

## VDXExt

Extracts media content from VDX files.

```
Usage:  VDXExt <VDXFiles> [/avi] [/sync]

    VDXFiles        Specifies the VDX files to be processed. VDXExt will
                        extract still images, video delta frames and audio files
                        as they appear within each VDX file. Wildcards are
                        allowed.
	avi             Causes VDXExt to convert all frames and an eventually
                        created wave file into an AVI video. The source frames
                        are deleted afterwards. Since the AVI is created using
                        uncompressed RGB images, the creation process is very
                        slow and produces huge amounts of data.
	sync            For synchronisation purposes, you may allow VDXExt to
                        repeat certain audio and/or video frames. This is useful
                        in conjunction with the /avi switch. Note that the end
                        of the audio or video stream will be padded should one
                        of them be longer than the other. Additionally, VDXExt
                        will be caused to create a silent audio stream if none
                        exists in the source VDX file.
```

# License

Copyright (C) 2000-2006, Deniz Oezmen (http://oezmen.eu/)

All rights reserved.

Redistribution and use in source and binary forms, with or without modification,
are permitted provided that the following conditions are met:

- Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
- Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
- Neither the name of the copyright holders nor the names of contributors may be used to endorse or promote products derived from this software without specific prior written permission.

```
THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```