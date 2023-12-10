---
title: "PSG"
date: 2023-12-03T19:36:27+02:00
draft: false
---
![image](/img/dev_psg.png)


## Channels

### Pulse


### Ramp

### Noise
The noise channel doesn't have a pulse width 


## Envelope
{{% notice style="tip" %}}
By default, the envelope does nothing. You can safely ignore it, if you don't want to use it.
{{% /notice %}}

Each channel has an _envelope generator._ This allows automated control for some parameters, such as volume and pitch. It has two memory mapped registers: _mask,_ and _length_. Mask is a bitmask for envelope settings, and length controls the length of the envelope.

### Envelope Mask

| Flag name        | Bit | Description                                                                     |
| ---------------- | --- | ------------------------------------------------------------------------------- |
| FLAG_VOL         | 0   | Controls Volume (Manual volume control still applies over this).                |
| FLAG_PW          | 1   | Controls Pulse Width / Duty Cycle  (Overrides manual control).                  |
| FLAG_FREQ        | 2   | Controls Pitch (sweep effect).                                                  |
| FLAG_GATE        | 3   | Enable Gate: Mute when timer runs out. Independent from volume flag.            |
| FLAG_FALLING     | 4   | Falling instead of rising: Envelope goes from 100% to 0% instead of 0% to 100%. |
|                  | 5   | unused                                                                          |
| FLAG_LOOP        | 6   | Envelope loops. Envelope starts over if it runs out.                            |
| FLAG_LOOP_MIRROR | 7   | If looping, every other cycle is reversed (rise-fall-rise-fall...).             |

Default value for mask is 0, meaning that no bits are set.


## Memory Map
| Addr | Global | Access | Name           | Description                             |
| ---- | ------ | ------ | -------------- | --------------------------------------- |
| 0x00 | todo   | W      | ch0_freq       | Pulse 0 Frequency in Hz                 |
| 0x01 | 0x01   | W      | ch0_vol        | Pulse 0 Volume                          |
| 0x02 | 0x02   | W      | ch0_pw         | Pulse 0 Pulse width                     |
| 0x03 | 0x03   | W      | ch0_env_mask   | Pulse 0 Envelope mask                   |
| 0x04 | 0x04   | W      | ch0_env_length | Pulse 0 Envelope length in milliseconds |
| ...  |        |        |                |                                         |
| 0x10 | 0x10   | W      | ch1_freq       | Pulse 1 Frequency in Hz                 |
| 0x11 | 0x11   | W      | ch1_vol        | Pulse 1 Volume                          |
| 0x12 | 0x12   | W      | ch1_pw         | Pulse 1 Pulse width                     |
| 0x13 | 0x13   | W      | ch1_env_mask   | Pulse 1 Envelope mask                   |
| 0x14 | 0x14   | W      | ch1_env_length | Pulse 1 Envelope length in milliseconds |
| ...  |        |        |                |                                         |
| 0x20 | 0x20   | W      | ch2_freq       | Ramp Frequency in Hz                    |
| 0x21 | 0x21   | W      | ch2_vol        | Ramp Volume                             |
| 0x22 | 0x22   | W      | ch2_dc         | Ramp Duty cycle                         |
| 0x23 | 0x23   | W      | ch2_env_mask   | Ramp Envelope mask                      |
| 0x24 | 0x24   | W      | ch2_env_length | Ramp Envelope length in milliseconds    |
| ...  |        |        |                |                                         |
| 0x30 | 0x30   | W      | ch3_freq       | Noise Frequency in Hz                   |
| 0x31 | 0x31   | W      | ch3_vol        | Noise Volume                            |
| 0x33 | 0x33   | W      | ch3_env_mask   | Noise Envelope mask                     |
| 0x34 | 0x34   | W      | ch3_env_length | Noise Envelope length in milliseconds   |

## Examples

Todo