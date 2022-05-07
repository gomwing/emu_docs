  Hardware Documentation

PC Engine Hardware : PSG
_<div style="text-align: right">by Paul Clifford (paul@plasma.demon.co.uk)</div>_

__Introduction :__

The PSG provides 6 sound channels, which can be conveniently paired according to the functionality they provide :

|     |     |     |
| --- | --- | --- |
| 0-1 | -   | Waveform playback  <br>Frequency modulation (channel 1 muted) |
| 2-3 | -   | Waveform playback only |
| 4-5 | -   | Waveform playback  <br>White noise generation |

Waveform playback is the most common and allows a 32-byte, 5-bit unsigned linear sample to be played back at selected frequencies. Frequency modulation takes this one step further, allowing the playback frequency to be dynamically adjusted according to a specified pattern. White noise is used to simulate percussion instruments and effects such as explosions, by means of a pseudo random square wave.

Alternatively, each channel can be individually switched to "Direct D/A" mode whereby the programmer can send data directly to the sound mixer, allowing more complex sound patterns to be generated, such as speech. Inevitably this requires more programming effort and CPU time.

__PSG registers :__

| **Channel select**||||
| --- | --- | --- | --- |
| `$0800` | ` /W` | bit 7-3 : | (unused) |
| bit 2-0 : | Channel number (only 0-5 valid) |

This selects the channel used for operations on registers `$0802` to `$0807`. Be aware that the noise register is only valid for channels 4 and 5, and that the LFO registers will affect channels 0 and 1 only, irrespective of what values you set here.

| **Global sound balance** |     |     |     |
| --- | --- | --- | --- |
| `$0801` | ` /W` | bit 7-4 : | Volume from left output |
| bit 3-0 : | Volume from right output |

This alters the overall sound volume once all the channels have been mixed together.

| **Fine frequency adjust** |     |     |     |
| --- | --- | --- | --- |
| `$0802` | ` /W` | bit 7-0 : | The lower 8 bits of the 12 bit channel frequency |

The channel frequency is a 12 bit value used as a divider into the 3.58MHz clock. The exact use depends on what type of sound the channel is being used for at the time. For waveform output, a copy of this value is, in effect, decremented 3,580,000 times a second until zero is reached. When this happens the PSG advances an internal pointer into the channel's waveform buffer by one. Since the buffer is 32 bytes long, this frequency value can be converted into more familiar units as follows :
```
                         3580000
 frequency (Hz) = ---------------------
                   32 x (12 bit value)
```
Hence, in the opposite direction we would have :
```
                       3580000
 12 bit value = ---------------------
                 32 x frequency (Hz)
```
  

| **Rough frequency adjust** |     |     
| --- | --- | 
| `$0803` | ` /W` 
| bit 7-4 : | (unused) |
| bit 3-0 : | The upper 4 bits of the 12 bit channel frequency |

See above for explanation.

| **Channel on/off, DDA on/off, channel volume** |     |    
| --- | --- | 
| `$0804` | ` /W` 
| bit 7 : | Channel on (1) or off (0) |
| bit 6 : | DDA output on (1) or off (0) |
| bit 5 : | (unused) |
| bit 4-0 : | Overall channel volume |

Depending on the setting of bit 6 and 7, a channel can be in one of four states:

|`ch on`| dda | state |
| --- | --- | --- |
| 0   | 0   | Writes to `$0806` will store the value in the waveform buffer and advance the waveform write index. |
| 0   | 1   | The waveform write index is reset to 0, so that further writes to `$0806` will start from the beginning of the waveform buffer. |
| 1   | 0   | Waveform output is enabled. The channel output is generated from the waveform buffer, advancing an internal read index at the rate specified by the channel frequency registers (`$0802` and `$0803`). |
| 1   | 1   | Direct D/A mode enabled. Any value written to `$0806` is immediately mixed into the overall sound output. |

The overall channel volume can be used to fade in and out individual channels (see `$0805` for altering channel balance).

| **Channel balance** |     |     
| --- | --- | 
| `$0805` | ` /W` 
| bit 7-4 : | Volume to left output |
| bit 3-0 : | Volume to right output |

This allows you to alter the balance of an individual channel.

| **Channel sound data** |     |
| --- | --- | 
| `$0806` | ` /W` 
| bit 7-5 : | (unused) |
| bit 4-0 : | 5 bit unsigned linear sample data |

A write to this location will have different effects depending on the settings of bit 6 and 7 of register `$0804`. When DDA is enabled, data written here is mixed in directly with the outputs from the other channels (you also need to turn the channel on if you actually want to hear it though!). This is useful for handling things like speech which are not easy (possible?) to do with the waveform buffer.

When the channel is turned off and DDA disabled, data written here is copied into the channel's waveform buffer and the internal write index incremented by one, wrapping round at 32 to 0. For example, to make a sine wave you could write the following hex values into the waveform buffer (shamelessly plundered from the PSG patent) :

      0f, 12, 15, 17, 19, 1b, 1d, 1e,
      1e, 1e, 1d, 1b, 19, 17, 15, 12,
      0f, 0c, 09, 07, 05, 03, 01, 00,
      00, 00, 01, 03, 05, 07, 09, 0c

 
| **Noise enable, noise frequency** |     |
| --- | --- |
| `$0807` | ` /W` 
| bit 7 : | Noise on (1) or off (0) |
| bit 6-5 : | (unused) |
| bit 4-0 : | Noise frequency |

This register is only effective for channels 4 and 5. The output of white noise is enabled by setting bit 7, at which point the PSG will stop reading data from the channel's waveform buffer and begin generating a random rectangular waveform with a frequency defined by the lower 5 bits of the register.

After a little experimenting I found that it is easiest to imagine you are dealing with a 64-byte waveform buffer divided into two parts. The first half randomly contains either all 0 or all 31, and likewise with the second half, so that you have either a complete or a partial cycle of a square wave, ie one of the following :
```
 ----+            +----   ---------
     |            |
     +----    ----+                   ---------
 0  32  64    0  32  64   0  32  64   0  32  64
```
_(A new "waveform" is automatically generated each time the read index wraps back around to zero)._

Contrarily to the channel frequency, the noise frequency field is bit inverted, so it is necessary to XOR it by 31 (`%11111`) for correct results.

The formula for the actual noise frequency is therefore :
```
                           3580000
 frequency (Hz) = ---------------------------
                   64 x (5 bit value XOR 31)
```
Hence, in the opposite direction we would have :
```
                      3580000
 5 bit value = --------------------- XOR 31
                64 x frequency (Hz)
```
  

| **LFO frequency** |     |
| --- | --- |
| `$0808` | ` /W` 
| bit 7-0 : | LFO frequency |

When the LFO is active (see `$0809`), the channel 1 waveform buffer is assumed to contain frequency modulation data rather than samples (and hence channel 1 is automatically muted). The frequency at which this buffer is read from is defined by multiplying the LFO frequency by the 12 bit frequency (`$0802` and `$0803`) from channel 1. This leads to the following formula :
```
                         3580000
 freq (Hz) = ---------------------------------
              32 x (12-bit freq) x (LFO freq)
```
The values in channel 1's waveform buffer are treated as 5-bit signed integers which are shifted left as necessary (see `$0809`) and added to channel 0's frequency. This result then becomes the new frequency for channel 0 until a new byte of FM data is read, at which point the frequency is recalculated again.

| **LFO trigger, LFO control** |     |
| --- | --- |
| `$0809` | ` /W` 
| bit 7 : | LFO trigger  <br>(0 = LFO on, 1 = LFO off/reset) |
| bit 6-2 : | (unused) |
| bit 1-0 : | LFO control |

Bit 7 controls whether the low frequency oscillator (LFO) is active or not. When set it causes the LFO to switch off and resets the channel 1 waveform read position to 0. When clear, the LFO is activated, causing the data in channel 1's waveform buffer to be used to frequency modulate the output from channel 0. The process by which this is achieved depends on the value in "LFO control" (the lower two bits) :

|     |     |     |
| --- | --- | --- |
| 00  | -   | No frequency modulation is performed, so the output from channel 0 is unchanged. |
| 01  | -   | The FM data is added directly to channel 0's frequency. |
| 10  | -   | The FM data is shifted left by four places then added to the frequency. |
| 11  | -   | The FM data is shifted left by eight places then added to the frequency. |

For example, if "LFO control" was set to 2 and the value read from the channel 1 waveform buffer was binary `%10111` then (-9 << 4) would be added to channel 0's frequency.

  

![](magickit.gif)