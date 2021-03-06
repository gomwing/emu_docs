
Ultimate Soundtracker module format description
=============================================================================

This is  an attempt  on documenting  the file  format of music modules
(MOD  files)  that  were  created  with  Karsten  Obarski's   Ultimate
Soundtracker, the original  Soundtracker that started  it all back  in
1987/88 on AMIGA.

Whereas  various   Soundtracker  derivatives   such  as    Protracker,
Noisetracker,  or  a  few  of  the  Soundtracker v2 series, are widely
known and supported, hardly  any available MODule player  supports old
and classic Soundtracker modules.

In  1988  and  later  Karsten  Obarski's  original program was hacked,
ripped  off,  and  improved  by  various programmers from cracking and
demo groups.  Some of the  first were Exterminator of TJC, Tip  of The
New  Masters,  Unknown/D.O.C,  Mahoney  &  Kaktus  of  Northstar   and
Silents, and Mnemotron/Spreadpoint.  During this process the  original
module  format  got  altered  and  extended.   One  by-product of this
development   was    partial   incompatibility    between    competing
Soundtrackers and their modules,  most noticably between the  Ultimate
Soundtracker and  the first  illegal series  of Soundtracker versions.
Even  worse,  some  changes  made  it  impossible  -  or at least very
difficult - to detect the true module format.

Years later  people without  knowledge of  the incompatibility between
the  original   Soundtracker  module   format  and   successors   like
Soundtracker 2.4 or Protracker  damaged modules by converting  them to
Protracker  format.   It  would  be  tiresome  trying to find any such
module in any  collection and either  repair or remove  it in case  it
can't be restored properly.  However, the opposite doesn't seem to  be
a real choice either.  Rather than trying to find and convert any  old
Soundtracker module  into some  well-defined module  format, it sounds
much more reasonable  to add native  Ultimate Soundtracker support  to
MODule players.

Old Soundtracker modules  that are likely  to be found  in any classic
collection  are  those  composed  by  Karsten Obarski himself, such as
famous game sounds from  Amegas, Crystal Hammer, Ralleymaster  (sic!),
or Sarcophaser, to name a few, and others done in 1987 and 1988,  most
noticably the unforgotten tunes by SLL.

Rather  than  serving  as  a  complete  MOD  reference,  this document
focuses  on  relevant  differences  between  the Ultimate Soundtracker
format and the first  popular hacked Soundtracker versions  that still
featured  4  voices  and  15  channels.   The terminology used in this
document might differ from other available MOD format descriptions.

The following abbreviations are  local to this document.  Please don't
use them in MOD players. They are uncommon and would confuse users.

 UST -> Ultimate Soundtracker
 ST  -> Soundtracker (scene versions)
 MST -> Master Soundtracker
 PT  -> Protracker
 NT  -> Noisetracker

One false assumption often made is that "M.K." is an ID introduced  in
Protracker or by "Mahoney & Kaktus".  The truth is it was  Unknown/DOC
who put his initials into Soundtracker 2.4 to server as format ID  and
indicate 31 samples.  Mahoney & Kaktus used "N.T." in Noisetracker.

Thanks  to  Jake  Stine  (MikMod)  and  Lada Kopecky (A.M.P) for their
interesting discussions about UST format detection proposals.

If you have any comments or corrections, feel free to e-mail me.

-----------------------------------------------------------------------------

Short summary of differences and incompatibilities (more below):

 - maximum sample length
 - numbering of effects
 - playing of repeat-samples (looping samples)

Format characteristics:

 - 4 tracks (voices, channels)
 - 15 sample headers (instrument definitions, slots)
 - sample header length is 30 bytes
 - 128 pattern table steps (pattern order)
 - pattern length is 1024 bytes

File offset         Content description

 + 0                song/module working title
 + 20               15 sample headers (see below)
 + 470              song length (number of steps in pattern table)
 + 471              song speed in beats per minute (see below)
 + 472              pattern step table
 + 600              pattern data (1024 bytes) for each pattern number
 .                  that can be found in entire pattern table
 .
 + ???              sample data


Sample header (big-endian byte order):

 + 0  sample file/name
 + 22 sample length in words
 + 24 volume word (0-64)
 + 26 sample repeat offset in bytes
 + 28 sample repeat length in words (0=loop off, >1 loop on)
[+ 30 (end)]


Noticable features in sample header:

 - Volume word does not contain a "Finetuning" value in its high-byte.

 - Sample repeat offset is in bytes (unlike PT, NT, and ST 2.5, where
   it is specified as number of words).

 - Maximum sample length is 9999 bytes decimal, but 1387 words hexadecimal.
   Longest samples on original sample disk ST-01 were 9900 bytes.

 - Sample file names have no disk name prefix like "st-01:" or "ST-01:"
   since only a single sample disk was supported. In later ST versions
   one had to enter a disk name.

   Caveat: There are hacked modules where disk names have been
           dropped or added.

Notes on playing repeat-samples:

 - Unlike PT only the loop-area is played. PT plays from Start to Repeat
   End and then loops between Repeat Start and Repeat End. UST modules
   often (!) sound screwed if repeat-samples are played incorrectly.
   Hence: Sample Start = Repeat Start, Sample Length = Repeat Length.

Effects:

 - Arpeggio: 1xy (1. base note)
                 (2. x semitones higher)
                 (3. y semitones higher)

 - Pitchbend: 2xy (20y = sub y from period = pitch up)
                  (2x0 = add x to period = pitch down)

Conversion of UST effects to PT (or MST):

 - Arpeggio:  1xy => 0xy

 - Pitchbend: 20y => 10y
              2x0 => 20x

-----------------------------------------------------------------------------

Song speed in beats per minute:

The byte at module offset 471  is not the "song restart position".  It
is meant to be  the song speed in  beats per minute (bpm),  satisfying
this formula:

  AMIGA Timer-IRQ value = (240-bpm)*122

This might  be constant  for other  15-instrument ST  modules, but not
for the Ultimate Soundtracker.

The default for UST  modules is 0x78 =  120 BPM = 48  Hz. AMIGA custom
chips only ran at 716 kHz,  which is one tenth of the  processor clock
speed.  Thus:

  freq = 716 kHz / ((240-bpm)*122)
  [freq] = kHz

Rumours state  that Karsten  Obarski made  a failure  upon calculating
that default speed and planned to get a default of 50 Hz. For sure  he
didn't calculate  at full  precision.   This would  have required  the
true accurate clock speed of the  AMIGA.  And that one was  varying in
different documentation.  If you happen to find a more accurate  clock
speed, the result might differ by 1-2 Hz more. Look:

  with 716 kHz = 716*1024 Hz : freq(120) ~= 50.08 Hz
  with 716 kHz = 716*1000 Hz : freq(120) ~= 48.9 Hz

-----------------------------------------------------------------------------

An experimental format detection:

Note that the recommended way is  to either default to UST or  provide
a switch to  toggle between UST  and ST. The  fact that an  UST module
can't  be  detected  100%  percent  correctly,  can't  make  MODplayer
authors happy. But think about a switch at least.

 - Check whether every Sample Length is <= 9999 bytes. If not, the
   MOD cannot be in UST format. Newer Sountrackers supported samples
   longer than 9999 bytes. So, it might be in some newer ST format.

   Caveat: It still could be a ST, MST or PT module with short samples.

 - If (Repeat Offset in words + Repeat Length in words) converted to
   bytes exceeds Sample End and/or length of file, it is an UST file
   with Repeat Offset in bytes. In other words, first assume Repeat
   Offset to be given in words and calculate the Repeat End in order
   to be able to check the sample range:

     Sample Start + Repeat Offset * 2 = Repeat End

   If this Repeat End exceeds the sample end, it is an UST module and
   Repeat Offset is specified in bytes.

   Caveat: The looping in some ST modules (bad rips, for instance)
   could go a couple of bytes past the end, so better add some safety
   bytes.

 - If you use a format loader/converter, scan each pattern for the
   availability of PT effects or any effects other than 1xy and 2xy.
   If available it cannot be UST.

   Might be an idea to check the pattern data for effects 1xy and 2xy
   with xy > 0x1f. Could be that no Soundtracker module would ever have
   a reason to pitchbend up or down that far, while almost any UST module
   that uses either effect does so. The exception would be a UST module
   that uses only 20y / 21x commands or a very low arpeggio.

Of  course,  the  only  exception  to  the  rule  now  is  if  a newer
SoundTracker module doesn't  follow the sample  prefix rules, has  all
samples < 9999 bytes, uses no effects at all, and has a loop near  the
start of a sample only. A more advanced detection could check  whether
the samples are from the ST-01 sample disk preset.

Master  Soundtracker  1.0  introduced  new  effects and changes effect
numbering.

Soundtracker 2.0  was based  on Master  Soundtracker 1.0. Soundtracker
2.0, 2.1, 2.2, 2.3, 2.4 have Repeat Offset specified in bytes.  As  of
Soundtracker  2.5  Repeat  Offset  is  in  words.   Soundtracker   2.3
introduced  31  samples.   Soundtracker  2.4  introduced Unknown/DOC's
initials  "M.K."  as   format  ID.  Soundtracker   2.6  introduced   a
double-sized  pattern  order  table  and  the  "MTN"  format  ID  from
Mnemotron.

In  Noisetracker   1.0,  Repeat   Offset  is   specified  in    words.
Noisetracker features 31 samples and the "N.T." ID.

-----------------------------------------------------------------------------
