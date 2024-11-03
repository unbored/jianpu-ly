# jianpu-ly:Guqin

Lilypond编译简谱，[原作者ssb22](https://github.com/ssb22/jianpu-ly)。针对古琴谱的特点进行了修改调整。

一个Python程序，利用Lilypond的排版系统生成简谱。使用本脚本需要基本的Python程序运行和Lilypond乐谱编译知识。

目前在Python3和Lilypond 2.24版本下编译通过。

使用方法：
```
python3 jianpu-ly [txt文件] > [ly文件]
lilypond [ly文件]
```

支持的指令列表：

音符：`1 2 3 4 5 6 7 0`

升降调：`1 #2 3 b4`

八度：`1,, 2' ,3 ''4`

八分、十六分、三十二分、六十四分音符：`q1 s1 d1 h1`

附点：`q1. s2`

延长线（二分、二分附点、全音符）：`1 - 2 - - 3 - - -`

拍号（默认不显示，但会进行小结检查）：`2/4` `3/8`

调号：`1=Bb` `6=C`

速度：`4=86` `8=40`

歌词：`L: 天 地 玄 黄 ~ 宇宙 洪荒`

谱头：
```
title=主标题
subtitle=副标题
composer=作曲者（右上）
arranger=整理者（右下）
poet=调式（左上）
1=F
meter=调弦方式（左下）
strings=5,, 6,, 1, 2, 3, 5, 6,
```

乐谱开始：`BeginScore`

乐谱分节：`NextScore`

节标题：`piece=标题`

关闭小节数显示：`NoBarNums`

关闭首行缩进：`NoIndent`

连音：`3[ q1 q1 q1 ]` `5[ s1 s2 s3 s4 s5 ]`

装饰音：`G{ s1 s2 } 3` `G{ s1 ( s2 } 3 )`

后装饰音：`1 AG{ s2 s3 }` `1 ( AG{ s2 s3 ) }`

和弦（八度、升降等应放在数字前，中间没有空格。自动根据音高排序）：`,1,3,5` `''1'#4`

反复记号（可选不同结尾）：`R{ 1 1 1 } A{ 2 | 3 }`

连音线：`1 ~ 1`

联结线：`1 ( 2 3 ) 4`

上滑音（绰）下滑音（注）：`1 \upArrow 2 \downArrow`

力度：`1 \p 2 \mf`

其他单音标记（自由延长、泛音）：`1 \fermata 2 \flageolet`

整组泛音：
```
1
Harm:
2 3 4
:Harm
5
```

Markup标记（可附在一行最后）：`1 M_\line{"测试" "文本"}`

单行注释：`% 注释`

示例文件（结合JianziNote程序）：
```
% jianpu-ly.py 文檔
title=主标题
subtitle=副标题
composer=流素鳴桐作曲
arranger=流素鳴桐整理
poet=蕤宾调
1=Bb
meter=紧五弦
strings=2,, 3,, 5,, 6,, 1, 2, 3,

BeginScore

4=44
4/4
1,    M_\"jz:散挑七"
G{
s1, ( M_\"jz:历六五"
s2,
}
2,  ) M_\"jz:勾四"
,3,5  M_\"jz:拨三二"
-
```

# jianpu-ly

Jianpu in Lilypond, from http://ssb22.user.srcf.net/mwrhome/jianpu-ly.html

(also mirrored at http://ssb22.gitlab.io/mwrhome/jianpu-ly.html just in case, and available via `pip install jianpu-ly` or `pipx run jianpu-ly`)

jianpu-ly is a Python program (compatible with both Python 2 and Python 3) that assists with printing jianpu (numbered musical notation) in the GNU Lilypond music typesetter. The jianpu is written on a modiﬁed-appearance “stave” in Lilypond, which means Lilypond’s typesetting capabilities (lyric spacing, slurs, beams etc) will apply to the jianpu without needing to add a 5-line stave. If you prefer, the generated code for the jianpu stave may also be placed in a score with other types of stave.

Using jianpu-ly requires some technical knowledge.  If you don't know what a command line is, what a text editor is, what a directory is or what Python is, then please find out about these things before attempting to use jianpu-ly.  It is not an extension to Lilypond front-ends like Frescobaldi; it is a preprocessor that currently requires you to have command-line experience.

If you have problems, try a different Lilypond version.
jianpu-ly works with Lilypond 2.18, 2.20, 2.22 and 2.24.

Run jianpu-ly < text-file > ly-file (or jianpu-ly text-files > ly-file)

Text files are whitespace-separated and can contain:

Scale going up: `1 2 3 4 5 6 7 1'`

Accidentals: `1 #1 2 b2 1`

Octaves: `1,, 1, 1 1' 1''`

Shortcuts for 1' and 2': `8 9`

Percussion beat: `x`

Change base octave: `< >`

Semiquaver, quaver, crotchet (16/8/4th notes): `s1 q1 1`

Dotted versions of the above (50% longer): `s1. q1. 1.`

Demisemiquaver, hemidemisemiquaver (32/64th notes): `d1 h1`

Minims (half notes) use dashes: `1 -`

Dotted minim: `1 - -`

Semibreve (whole note): `1 - - -`

Time signature: `4/4`

Time signature with quaver anacrusis (8th-note pickup): `4/4,8`

Key signature (major): `1=Bb`

Key signature (minor): `6=F#`

Tempo: `4=85`

Lyrics: `L: here are the syl- la- bles` (all on one line)

Lyrics (verse 1): `L: 1. Here is verse one`

Lyrics (verse 2): `L: 2. Here is verse two`

Hanzi lyrics (auto space): `H: hanzi` (with or without spaces)

Lilypond headers: `title=the title` (on a line of its own)

Guitar chords: `chords=c2. g:7 c` (on own line)

Fret diagrams: `frets=guitar` (on own line)

Multiple parts: `NextPart`

Instrument of current part: `instrument=Flute` (on a line of its own)

Multiple movements: `NextScore`

Prohibit page breaks until end of this movement: `OnePage`

Suppress bar numbers: `NoBarNums`

Suppress first-line indent: `NoIndent`

Ragged last line: `RaggedLast`

Old-style time signature: `SeparateTimesig 1=C 4/4`

Indonesian 'not angka' style: `angka`

Add a Western staff doubling the tune: `WithStaff`

Tuplets: `3[ q1 q1 q1 ]`

Grace notes before: `g[#45] 1`

Grace notes after: `1 ['1]g`

Grace notes with durations: `g[d4d5s6] 1`

Simple chords: `,13'5 1 1b3 1` (chord numbers are sorted automatically)

Da capo: `1 1 Fine 1 1 1 1 1 1 DC`

Repeat (with alternate endings): `R{ 1 1 1 } A{ 2 | 3 }`

Short repeats (percent): `R4{ 1 2 }`

Ties (like Lilypond's, if you don't want dashes): `1 ~ 1`

Slurs (like Lilypond's): `1 ( 2 )`

Erhu fingering (applies to previous note): `Fr=0 Fr=4`

Erhu symbol (applies to previous note): `souyin harmonic up down bend tilde`

Tremolo: `1/// - 1///5 -`

Rehearsal letters: `letterA letterB`

Multibar rest: `R*8`

Dynamics (applies to previous note): `\p \mp \f`

Other 1-word Lilypond \ commands: `\fermata \> \! \( \) etc`

Text: `^"above note" _"below note"`

Harmonic symbols above main notes: `Harm: (music) :Harm` (main music)

Other Lilypond code: `LP: (block of code) :LP` (each delimeter at start of its line)

Unicode approximation instead of Lilypond: `Unicode`

Ignored: `% a comment`


Copyright and Trademarks
------------------------

(c) Silas S. Brown, licensed under Apache 2.

Apache is a registered trademark of The Apache Software Foundation.
Python is a trademark of the Python Software Foundation.
Any other trademarks I mentioned without realising are trademarks of their respective holders.
