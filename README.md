# px4_tunes
Tune library for PX4 compatible vehicles
## How to use
* Go to your `Firmware/boards/...` directory ( in case of a fmu_v2, `Firmware/boards/px4/fmu-v2` )
Example: `cd ~/src/Firmware/boards/px4/fmu-v2`
* Open the desired `cmake` file
Example: `gedit multicopter.cmake`

* Enable the `tone alarm` driver (and `tune_control` systemcmd, for testing)
(remove hashtag in front of lines, uncomment)

* Open /Firmware/src/lib/tunes/tune_definition.desc file
It will show you all default tunes, take a look and check out the patterns

* Copy and paste the `tune_definition.desc` file above, replacing the previous

* Build firmware and upload with `make [firmware_version] upload`
Example: `make px4_fmu-v2_multicopter upload` to build the multicopter version


### Those are the rules for the musical expressions, according to PX4

#### Driver for the PX4 audio .
The tune_control supports a set of predefined "alarm" tunes and
one user-supplied tune.

Tunes follow the syntax of the Microsoft GWBasic/QBasic PLAY
statement, with some exceptions and extensions.

From Wikibooks:

PLAY "[string expression]"

Used to play notes and a score ... The tones are indicated by letters A through G.
Accidentals are indicated with a "+" or "#" (for sharp) or "-" (for flat)
immediately after the note letter. See this example:

  PLAY "C C# C C#"

Whitespaces are ignored inside the string expression. There are also codes that
set the duration, octave and tempo. They are all case-insensitive. PLAY executes
the commands or notes the order in which they appear in the string. Any indicators
that change the properties are effective for the notes following that indicator.

* Ln     Sets the duration (length) of the notes. The variable n does not indicate an actual duration
       amount but rather a note type; L1 - whole note, L2 - half note, L4 - quarter note, etc.
       (L8, L16, L32, L64, ...). By default, n = 4.
       For triplets and quintets, use L3, L6, L12, ... and L5, L10, L20, ... series respectively.
       The shorthand notation of length is also provided for a note. For example, "L4 CDE L8 FG L4 AB"
       can be shortened to "L4 CDE F8G8 AB". F and G play as eighth notes while others play as quarter notes.
* On     Sets the current octave. Valid values for n are 0 through 6. An octave begins with C and ends with B.
       Remember that C- is equivalent to B.
* < >    Changes the current octave respectively down or up one level.
* Nn     Plays a specified note in the seven-octave range. Valid values are from 0 to 84. (0 is a pause.)
       Cannot use with sharp and flat. Cannot use with the shorthand notation neither.
* MN     Stand for Music Normal. Note duration is 7/8ths of the length indicated by Ln. It is the default mode.
* ML     Stand for Music Legato. Note duration is full length of that indicated by Ln.
* MS     Stand for Music Staccato. Note duration is 3/4ths of the length indicated by Ln.
* Pn     Causes a silence (pause) for the length of note indicated (same as Ln).
* Tn     Sets the number of "L4"s per minute (tempo). Valid values are from 32 to 255. The default value is T120.
.      When placed after a note, it causes the duration of the note to be 3/2 of the set duration.
       This is how to get "dotted" notes. "L4 C#." would play C sharp as a dotted quarter note.
       It can be used for a pause as well.
 Extensions/variations:
 * MB MF  The MF command causes the tune to play once and then stop. The MB command causes the
       tune to repeat when it ends.
