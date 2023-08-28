# subtitle-converter

Convert DFXP to SRT, SSA format.

## Usage

```
positional arguments:
  input-files           subtitle files

optional arguments:
  -h, --help            show this help message and exit
  -o [output file], --output [output file]
                        output file with extension srt, ssa or ass
  -v, --version         displays the version of this application and exits
  --shift [ms]          increases all timestamps by the specified value. You
                        can use a negative number
  --scale-factor [number or label]
                        multiplies the timestamps by this mumber. You can use
                        also any of these labels: NTSC2PAL (23.976/25),
                        PAL2NTSC (25/23.976), NTSC2FILM (23.976/24), PAL2FILM
                        (25/24), FILM2NTSC (24/23.976), FILM2PAL (24/25)
  -l [language code], --lang [language code]
                        subtitle language code ('en', 'es', etc,). It's used
                        by the language filter
  -a [number], --video-aspect [number]
                        the aspect ratio of the video. It's used to calculate
                        the correct PlayResY and PlayResY options for the SSA
                        style. Default: 16/9
  --no-cosmetic-fix     disables a filter which makes some cosmetic changes,
                        like adding a space after the symbol '-' and the next
                        word
  --no-language-fix     disables a filter which can fix some wrong characters
                        in some specific languages
  --no-fix-amazon-errors
                        don't try to fix errors that may occur in subtitles
                        from Amazon
  -c [encoding], --charset [encoding]
                        the encoding of the input file
  --output-format [srt, ssa or vtt]
                        output format to use if an output file has not been
                        set
  -srt, --srt           equivalent to --output_format srt
  -vtt, --vtt           equivalent to --output_format vtt
  --no-italics          removes the italic tags from the dialog texts
  --no-top              all dialog will be displayed at the bottom of the
                        screen
  --ssa-fontname [font], -f [font]
                        the font name (default: arial)
  --ssa-fontsize [number], -fs [number]
                        the font size (default: 50)
  --ssa-primary-color [color], -pc [color]
                        the primary color in format AABBGGRR or color name
                        (default: white)
  --ssa-back-color [color], -bc [color]
                        the back color in format AABBGGRR or color name
                        (default: 40000000)
  --ssa-outline-color [color], -oc [color]
                        the outline color in format AABBGGRR or color name
                        (default: black)
  --ssa-bold, -b        the font will be in bold
  --ssa-italic, -i      the font will be in italic
  --no-timestamp-manipulation
                        no changes will be made on timestamps
  --no-fix-collisions   collisions on timestamps won't be fixed
  --no-remove-duplicated
                        duplicated texts won't be removed
  --min-sep-ms [ms]     minimum separation (in ms) between framestamps
                        (SSA/ASS output only)
```

If multiple subtitle files are supplied, the application will create the
output files using the input filenames, replacing the extension with srt or ssa.
Be carefull, if a file with the same output name already exists the application
will overwrite it without asking.

If an output filename is specified with the -o option, then only the first of
the input files will be converted, using the output filename.

### Common use cases

Simple conversion:

```bash
subconv subtitle.dfxp -o subtitle.ssa
```

or

```bash
subconv subtitle.dfxp -o subtitle.srt
```

Shift everything forward by 2 secs:

```bash
subconv --shift 2000 subtitle.dfxp -o subtitle.srt
```

Convert from one frame rate to another:

```bash
subconv --scale-factor 23.976/25 subtitle.dfxp -o subtitle.srt
```

or

```bash
subconv --scale-factor NTSC2PAL subtitle.dfxp -o subtitle.srt
```

Those examples will convert a subtitle made for a movie at 23.976 frames per second for a version sped up to 25 fps (very common in Europe).

Convert two subtitles:

```bash
subconv subtitle1.dfxp subtitle2.dfxp
```

That will convert the subtitles to subtitle1.ssa and subtitle2.ssa

Convert all subtitles in a folder:

```bash
subconv *.dfxp
```

All files with extension dfxp will be converted to ssa.

### Authors

subtitle-converter, based on [ttml2srt](https://github.com/Paco8/ttml2ssa) by Paco8.
License: LGPL-2.1
