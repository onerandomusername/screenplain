# About Screenplain

You're a hacker. The command line is your home. You know tools like grep, sed
and Git inside out. You have formed a symbiotic relationship with your text
editor. Those tools are powerful in the right hands. But you're also a
screenwriter. Screenwriting is much like programming. It's about structure and
form, and -- obviously -- about reading, writing and modifying huge amounts of
text. You don't want to use software that lacks the power of your hacking
tools just because you're writing a screenplay instead of a shell script.

Enter Screenplain.

Screenplain allows you to write a screenplay as a plain text file using
a format called [Fountain](http://fountain.io). Text files
are simple and supported by all text manipulation software. It's not just for
hackers, too. The simplicity of plain text allows you to easily view and edit
them on devices such as tablets and phones. No need for specific screenwriting
software.

The magic that Screenplain performs is to take your plain text file and
convert it to a good looking screenplay in an industry standard format.
Send that file off to your producer, agent, director or screenwriting
competition. The supported output formats are FDX  HTML, and PDF.

Screenplain can be used as a command-line application or a library.
An [Online version of Screenplain](http://www.screenplain.com) is also
available.

Note that Screenplain is under development and is missing features and
the master branch may not always work. I'm currently working on supporting
the whole [Fountain](http://fountain.io) specification. (Fountain
was previously known as "Screenplay Markdown" or "SPMD.")

## Installing

    pip install screenplain

To enable PDF output, install with the PDF extra (installs ReportLab):

    pip install 'screenplain[PDF]'

## Credits

Screenplain was coded by [Martin Vilcans](http://www.librador.com).

The CSS code that formats Screenplain's HTML output as something that
looks as much as a printed screenplay as is possible in HTML was
created by [Jonathan Poritsky](http://www.candlerblog.com/).

The [Fountain](http://fountain.io) file format is the result of a
collaboration between [Stu Maschwitz](http://prolost.com) and
[John August](http://johnaugust.com/).


## License

Screenplain is released under the [MIT license](http://www.opensource.org/licenses/mit-license.php).


## Developing

Set up virtual environment:

    python3 -m venv .venv
    . .venv/bin/activate
    pip install -r requirements.txt
    pip install -e .

After this, the `screenplain` command will use the working copy of your code.

To run unit tests and style checks, run:

    bin/test

## TODO

This library is a WIP and does not currently support the entire fountain spec.

Note that this spec is written in such a way to be a simplified spec of what fountain itself entails.
This is to ease with implementation and testing.

### Parser

#### Fountain v1.0

- [X] SCENE HEADINGS
  - [X] Scene headings with INT., EXT., I., or E.
  - [X] Scene headings forced with a single `.` followed by an alphanumeric character
- [ ] ACTION
  - [x] All default text, that doesn't meet critera for ANY other element
  - [x] Forced with `!`
  - [x] leading spaces and tabs are preserved
  - [ ] Preserve vertical whitespace
- [x] CHARACTERS
  - [x] a line entirely in upperspace, with one empty line before, and no empty line after
  - [x] Can be indented, will be cut from output
  - [x] “Character Extensions”–the parenthetical notations that follow a character name on the same line–may be in uppercase or lowercase:
  - [x] must include one alphabetical character
  - [x] can be forced with preceding `@`
- [X] DIALOGUE
  - [X] any text immediately following a character OR parenthetical element
- [X] PARENTHETICALS
  - [X] Parentheticals follow a Character or Dialogue element, and are wrapped in parentheses ().
- [x] DUAL DIALOGUE
  - [x] Dual, or simultaneous, dialogue is expressed by adding a caret ^ after the second Character element.
  - [x] Any number of spaces between the Character name and the caret are acceptable, and will be ignored. All that matters is that the caret is the last character on the line.
- [ ] LYRICS
  - [ ] Always forced
  - [ ] any line starting with `~`.
  - [ ] Not specific on whether this can be dialogue only...
    - [ ] implementing as if it must be dialogue.. For now.
- [x] TRANSITIONS
  - [x] Uppercase
  - [x] Preceded by and followed by an empty line
  - [x] Ending in TO:
  - [x] forced with: `>`
  - [ ] mustn't have trailing whitespace
- [x] CENTERED TEXT
  - [x] Action text, but centered
  - [x] forced with `>text<`.
  - [x] leading spaces NOT preserved
- [ ] EMPHASIS
  - [ ] <https://fountain.io/syntax/#emphasis>
- [x] TITLE PAGE
  - [x] The optional Title Page is always the first thing in a Fountain document. Information is encoding in the format key: value. Keys can have spaces (e. g. Draft date), but must end with a colon.
  - [x] basically, email header rules but with spaces in the key names too.
- [x] PAGE BREAKS
  - [x] `===`
- [ ] PUNCTUATION
  - [x] two spaces on a blank line continues the dialogue if it was preceeding.
  - [ ] Leading tabs or spaces in elements other than Action will be ignored
- [x] NOTES
  - [x] Wrapped with `[[text]]`
  - [x] Notes can contain carriage returns, but if you wish a note to contain an empty line, you must place two spaces there to “connect” the element into one.
  - [ ] do not appear in formatted output
- [x] BONEYARD
  - [x] Comments. `/* */`
  - [ ] do not appear in formatted output
- [ ] SECTIONS AND SYNOPSES
  - [x] Create a Section by preceding a line with one or more pound-sign # characters:
  - [ ] do not appear in formatted output.
  - [x] Synopses are single lines prefixed by an equals sign =. They can be located anywhere within the screenplay.
- [ ] ERROR HANDLING
  - [ ] MOST IMPORTANT
  - [ ] Fountain does its best to sensibly interpret the text file into screenplay formatting. When in doubt, Fountain returns text as Action. Better to show the writer what they wrote–in the wrong format–than skip over malformed text.
  - [ ] double line breaks reset the entire rendering engine. Exception may lie with two-spaced dialogue line.

#### Fountain v1.1

- [x] A Character element can by forced by preceding it by an “at” symbol @.
- [x] An Action element can by forced by preceding it by an exclamation point !.
- [ ] Lyrics are designated by a preceding tilde ~ on each line.
- [x] “Character Extensions”–the parenthetical notations that follow a character name on the same line–are no longer required to be uppercase.
- [ ] Two trailing spaces no longer forces an Action line.

## Future Plans

- [ ] Support for outputting formatted theatrical stage plays using the same syntax of Fountain.
- [ ] Optional Character/Location output and summaries.
- [ ] cheat-sheet synopses and note outputs. 
