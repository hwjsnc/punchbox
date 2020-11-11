punchbox
========

punchbox is a simple to use music box card creator. It will take a standard MIDI file and convert it into SVG files suitable for printing

Features
--------

* MIDI file reading
* Custom page size
* Reversible staves
* Custom music box definitions
* Automatic note transposition for best fit
* Multiple staves per page
* Cut markers with custom size
* Margin support

Note done yet:

* Gap analysis
* Note proximity


Example Render
--------------

![alt text](https://github.com/psav/punchbox/raw/master/mozart0.png "Example Render")

Installation
------------

To install, clone the repo, cd into it and then execute the following:

```
virtualenv -p python2 .pb2
source .pb2/bin/activate
pip install -U pip
pip install .
```

Configuration
-------------

The program is configured using the [YAML](https://en.wikipedia.org/wiki/YAML) file `punchbox.yaml`.
To add a music box, modify the associative array `boxen` in that file.
An example music box configuration is given below:

```
  35note:
    note_data: [60, 62, 67, 69, 71, 72, 74, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 98, 100]
    pitch: 2.0
    reverse: True
    note_collision: 5.0
```

A music box has the following properties:

* A name, i.e. `35note` in the example. This name can be given as an argument to the `--musicbox` switch in order to select the music box.

* `note_data`, an array of MIDI note numbers for each note, in the order they appear on the programming strip.
  MIDI note numbers correspond to a tone on the pentatonic scale.
  The tone A4 (usually at 440 Hz) usually corresponds to the value 69.
  Each halftone step up or down corresponds to an increase or decrease of the MIDI note number by one, respectively.
  A full table of MIDI note numbers can be found at http://www.music.mcgill.ca/~ich/classes/mumt306/StandardMIDIfileformat.html#BMA1_3.

* `pitch`: distance between two stave lines on the output paper.

* `reverse`: If `True`, the `note_data` is assumed to be to be given in reverse order compared to how they appear on the programming strip.

* `note_collision` specifies the minimum distance (in mm) of any two notes on the same line.

Other configuration options (independent of the music box) are given below.
These keys can also be changed with corresponding command line arguments.

* `divisor`: TODO.
  Something about the length of notes or the distance between them. Perhaps BPM?

* `filename`: The input MIDI file

* `transpose`: Minimum/maximum amount by which the piece may be transposed.

* `page`: Output page size (in mm).

* `margin`: Stave margin on all sides (in mm).

* `output`: Output file base name.
  The actual output files are named `[base name][page number].svg`.

* `font_size`: Font size of the page marker (in mm).

* `marker_offset`: Offset of the page marker (in mm).

* `marker_size`: Size of the markers (in mm).

* `default_musicbox`: Name of the music box data to assume if none is given as a command line argument.


Usage
-----

Once the music box is configured, run `.pb2/bin/punchbox` to generate an svg of the programming strip.

`punchbox` supports several command line arguments, notably:

* `--help` for a full list of flags

* `--filename` for the file name of the input MIDI file.

* `--output` for the output base file name.

* `--musicbox` to specify the music box.
