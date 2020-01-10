# Svgbob

<a href="https://crates.io/crates/svgbob"><img src="https://img.shields.io/crates/v/svgbob.svg" alt="svgbob’s current version badge" title="svgbob’s current version badge"></a><a href="https://travis-ci.org/ivanceras/svgbob">
<img src="https://api.travis-ci.org/ivanceras/svgbob.svg"/>
</a>

Svgbob is an ascii to svg converter.

There is a Work-in-Progress spec [here](https://github.com/ivanceras/svgbob/blob/master/spec.md)
Contribution to the spec is welcomed.

I've spent a huge time on developing the spec and implementation on my free-time.
If you like this project please consider supporting me on [patreon](https://www.patreon.com/ivanceras)

[Demo](http://ivanceras.github.io/svgbob-editor/)

[Docs](https://docs.rs/svgbob)


# Using in command line

`cargo install svgbob_cli`

`svgbob` normally operates on stdin and stdout:
```console
$ svgbob < examples/long.bob > long.svg
```
produces an SVG in `long.svg` similar to the one produced by the old `main` binary. `svgbob` also allows passing arguments instead:
```console
$ svgbob examples/long.bob -o long.svg
```
And you can mix and match:
```console
$ svgbob -o long.svg < examples/long.bob
$ svgbob examples/long.bob > long.svg
```

You can pipe string from the output of other program:
```console
echo -e "+--+\n| |\n+--+" | svgbob
```
You can also pass an inline string:
```console
svgbob -s -- "+--+\n| |\n+--+"
```

This is also documented in the output of `svgbob --help`:
```console

svgbob 0.2.5
SvgBobRus is an ascii to svg converter

USAGE:
    svgbob [FLAGS] [OPTIONS] [input] [SUBCOMMAND]

FLAGS:
    -h, --help       Prints help information
    -s               parse an inline string
    -V, --version    Prints version information

OPTIONS:
        --font-family <font-family>      text will be rendered with this font (default: 'arial')
        --font-size <font-size>          text will be rendered with this font size (default: 14)
    -o, --output <output>                where to write svg output [default: STDOUT]
        --scale <scale>                  scale the entire svg (dimensions, font size, stroke width) by this factor
                                         (default: 1)
        --stroke-width <stroke-width>    stroke width for all lines (default: 2)

ARGS:
    <input>    svgbob text file or inline string to parse [default: STDIN]

SUBCOMMANDS:
    build    Batch convert files to svg.
    help     Prints this message or the help of the given subcommand(s)

```




<img src="https://ivanceras.github.io/svgbob/svgbob/examples/demo.svg"/>

The SVG image is generated from the ascii text below.

```bob

Svgbob is a diagramming model
which uses a set of typing characters
to approximate the intended shape.

       .---.
      /-o-/--
   .-/ / /->
  ( *  \/
   '-.  \
      \ /
       '
It uses a combination of these characters
"which are readily available on your keyboards".

What can it do?

 o->  Basic shapes
                                                        .
       +------+   .------.    .------.      /\        .' `.
       |      |   |      |   (        )    /  \     .'     `.
       +------+   '------'    '------'    '----'     `.   .'
         _______            ________                   `.'   ^ /
        /       \      /\   \       \      ---->    | ^     / /
       /         \    /  \   )       )     <----    | |    / v
       \         /    \  /  /_______/               v |
        \_______/      \/

        .-----------.       .   <.      .>  .          ^  \
       (             )     (      )    (     )          \  \
        '-----+ ,---'       `>   '      `  <'            \  v
              |/


 o->  Quick logo scribbles
        .---.                      _
       /-o-/--       .--.         |-|               .--.
    .-/ / /->       /--. \     .--)-|    .--.-.    //.-.\
   ( *  \/         / O  )|     |  |-|    |->| |   (+(-*-))
    '-.  \        /\ |-//      .  * |    '--'-'    \\'-'/
       \ /        \ '+'/        \__/                '--'
        '          '--'

 o->  Even unicode box drawing characters are supported
            ┌─┬┐  ╔═╦╗  ╓─╥╖  ╒═╤╕
            ├─┼┤  ╠═╬╣  ╟─╫╢  ╞═╪╡
            └─┴┘  ╚═╩╝  ╙─╨╜  ╘═╧╛


 o->  Sequence Diagrams

                                   .--->  F
          A       B      C  D     /
          *-------*-----*---*----*----->  E
                   \            ^ \
                    v          /   '--->  G
                     B --> C -'


 o-> Statistical charts


    E +-------------------------*--+     E |                         o
    D |-------------------*--*--|--*     D |                   o  o  |  o
    C |-------------*--*  |  |  |  |     C |             o  o  |  |  |  |
    B |-------*--*  |  |  |  |  |  |     B |       o  o  |  |  |  |  |  |
    A +-*--*--+--+--+--+--+--+--+--+     A +-o--o--+--+--+--+--+--+--+--+
        5 10 15 20 25 30 35 40 45 50         5 10 15 20 25 30 35 40 45 50










 o->  Flow charts
                      .--.            .---.  .---. .---.  .---.    .---.  .---.
                      |  |   OS API   '---'  '---' '---'  '---'    '---'  '---'
                      v  |              |      |     |      |        |      |
             .-. .-. .-. |              v      v     |      v        |      v
         .-->'-' '-' '-' |            .------------. | .-----------. |  .-----.
         |     \  |  /   |            | Filesystem | | | Scheduler | |  | MMU |
         |      v . v    |            '------------' | '-----------' |  '-----'
         '_______/ \_____|                   |       |      |        |
                 \ /                         v       |      |        v
                  |     ____              .----.     |      |    .---------.
                  '--> /___/              | IO |<----'      |    | Network |
                                          '----'            |    '---------'
                                             |              |         |
                                             v              v         v
                                      .---------------------------------------.
                                      |                  HAL                  |
                                      '---------------------------------------'


 o->  Block diagrams

                          .-,(  ),-.
           ___  _      .-(          )-.
          [___]|=| -->(                )      __________
          /::/ |_|     '-(          ).-' --->[_...__...°]
                          '-.( ).-'
                                  \      ____   __
                                   '--->|    | |==|
                                        |____| |  |
                                        /::::/ |__|

 o-> Mindmaps

                                            .-->  Alpha
                                           /
                                          .---->  Initial Release
          Planning *-------.             /         \
                            \           /           '---> Patch 1
      Initial research       \         /             \
                *             \       /               '-->  Patch 2
                 \             \     .---------> Beta
                  \             \   /
                   \             o o                      _______
                    \          .---. o--.___             /       \
                     '------> (     )       '----*--->  . Release .
                               `---' o                   \_______/
                               o  o o \
                              /    \ \ \
                          .--'      \ \ \
                         /           \ \ '----+->  Push backs
                        .             \ \      \
                       /|              \ \      '----> Setbacks
                      / .               \ \
                     V /|                \ '-----> Reception
                Team  / .                 \
                     v /|                  \
             Worklaod / .                   '-->> Career change
                     V /
                 PTO  /
                     V
                 Bug


 o->  It can do complex stuff such as circuit diagrams


     +10-15V           ___0,047R
      *------o------o-|___|-o--o---------o----o-------.
             |      |       |  |         |    |       |
            ---     |       | .+.        |    |       |
      470uF ###     |       | | | 2k2    |    |       |
             | +    |       | | |        |    |      .+.
      *------o      '--.    | '+'       .+.   |      '-'
             |         |6   |7 |8    1k | |   |       |
            GND      .-+----+--+--.     | |   |       |
                     |            |     '+'   |       |
                     |            |1     |  |/  BC    |
                     |            +------o--+   547   |
                     |            |      |  |`>       |
                     |            |     ,+.   |       |
                     |            | 220R| |   o----||-+  IRF9Z34
                     |            |     | |   |    |+->
                     |  MC34063   |     `+'   |    ||-+
                     |            |      |    |       |  BYV29     -12V6
                     |            |      '----'       o--|<-o----o--X OUT
                     |            |2                  |     |    |
                     |            |--o                C|    |    |
                     |            | GND         30uH  C|    |   --- 470
                     |            |3      1nF         C|    |   ###  uF
                     |            |-------||--.       |     |    | +
                     '-----+----+-'           |      GND    |   GND
                          5|   4|             |             |
                           |    '-------------o-------------o
                           |                           ___  |
                           '------/\/\/------------o--|___|-'
                                                   |       1k0
                                                  .+.
                                                  | | 5k6 + 3k3
                                                  | | in Serie
                                                  '+'
                                                   |
                                                  GND

  .-------------.
 / Advantages: /
'-------------'
 -* Plain text format
    Ultimately portable, backward compatible and future proof.
 -* Degrades gracefully
    Even when not using a graphical renderer, it would still looks good
    as text based diagrams. Paste the text in your source code.
 -* Easiest to use. Anyone knows how to edit text.


  About Svgbob editor:
=======================

 -> The editor is a plain text editor in replace and block mode
    with smarter prediction on where you intended to type next.
      i.e: typing   / will move the cursor north east to continue the line.
 -> The editor also has an xray lens that reveals the underlying characters
    underneath that comprises the graph. Move the mouse around to see the characters
    that build up which image, while holding the mouse down
    momentarily cancels the xray

 .------------------------------.
( This page is editable. Try it! )
 '------------------------------'

+----------+
|   FAQ:   |
+----------+

   Q: "Why is there too much spacing on words"
   A: It is an intended behaviour as all the text are meant
      for labels. Each words of sentences corresponds to each separate text
      elements in the SVG output in order to maintain
      "a bit of alignment closes to their original location. *[0]"

   Q: Do people really type in diagrams in text, isn't that tedious?
   A: Using simple text editors to make text diagrams like these are really
      "tedious. Power users of vim or emacs can make diagrams with ease.*[1]"

   Q: Your editor sucks!
   A: That's the beauty of plain text.
      Use whatever editor you like.

   Q: "How to integrate this in markdown?"
   A: "There is a project called [Spongedown](https://ivanceras.github.io/spongedown)"
      which specifically does that. The svgbob diagramming feature is guarded
      with ```bob code block so as not to pollute the markdown syntax.


"Footnotes:"
"*[0]: Fonts mostly condensed words to look"
      and render nicely. Monospace fonts should have solved this
      problem, however the monospace fonts used in browsers
      are not really monospaced (i.e CJK full-width characters
      are only rendered 1.5x larger than ascii characters,
      "instead of 2x larger). In the terminal however, full-width"
      characters are rendered 2x larger using either monospace
      or non-monspaced fonts.

           .------------. | .-----------. |  .-----.   Look at that
           |  文件系统  | | |   调度器  | |  | MMU |   -------------->
           '------------' | '-----------' |  '-----'   monospace eh?

      Also using monofont on final output document makes it look like meant
      "something for devs, instead of documents for all."
      For a more heavy usage of text just use markdown format,
      "there is also [Spongedown](https://ivanceras.github.io/spongedown)"
      which allow you to write in markdown, combine it with svgbob diagrams,
      "together some other features like csv and math equations."

"*[1]  In vim, there is a drawIt plugin which helps you easily draw ascii"
      diagrams. For vim without using any plugins, you can use combination
      "of BLOCK mode editing(CTRL-v), REPLACE mode(SHIFT-r)",
      :set virtualedit=all to easily move the cursor everywhere,
      "cut, copy and paste text in block mode (<C-v> jjll 1vp)".
      For emacs: there is artist mode.

```

