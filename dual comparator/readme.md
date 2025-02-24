﻿# Dual Comparator

## Introduction

This 6HP dual module is a pair of simple comparator circuits, which turns triangle waves into a pulse waves with variable mark/space ratio. It takes two audio inputs and two control voltages, compares them, and outputs the result. If a CV is not patched, a variable voltage is used (derived from a voltage reference and a pot).

If the input waveform is a triangle wave, the output is a pulse wave with a variable mark-space ratio controlled by the CV.

I needed this because the Ondes Martenot has _two_ pulse waveforms: Gambe and Nasillard.
Gambe is roughly a pulse wave with 45% mark/space. (Petit gambe is a lowpass-filtered version of Gambe).
Nasillard is another pulse, but with around 5% mark/space.

![dual-comparator](images/panel-500.png)

## Features

- two audio ins (in2 normalized to in1)
- two PW cv ins (normalized to 5V)
- two pulse outputs
- two pots, for attenuverters

## Implementation

Choice of op-amp to use as comparator informed by [AN-849 Using Op Amps as Comparators](./AN-849.pdf) and in particular, transition time, overload recovery time and absence of phase reversal. A small amount of positive feedback provides some hysteresis to give clean switching even if the input signal has noise around the switching threshold.

- two trimmers, to null attenuverter
- low cost REF195 5V ref (direct to norm pots)
- two audio input buffers (2 audio) TL074
- two CV attenuverters (other half of 074)
- LT1213 dual op-amp as comparator
- 10k/15k resistive divider converts +/- 12V output to+/- 5V output. Volt swing and slew rate of comparator is reduced by current draw.
- two output buffers (TL072) with 47R output impedance.
- small pcb with just 2 pots. 6 jacks wired to pcb.

[Schematic (PDF)](schematic.pdf), [Eagle schematic](./Eagle/comparator.sch)

![board](./images/top.png) ([PDF](board.pdf)), [Eagle board](./Eagle/comparator.brd)

![completed module](images/pcb-600.jpg)]

[Bill of Materials](dual_comparator_BOM.md)

Front panel [FPD](./dual_comparator.fpd)

## Special Bonus Feature

This module was designed to sit next to an Intellijel Dixie 2 oscillator, providing an additional two pulse waveforms. The Dixie 2 has coarse and fine tune pots, and also on the PCB a three-pin connector for an optional, third, ultrafine tune. There was spare space on this module so I added a handy ultra-fine-tune pot. There are no jacks for this, use a 3-pin jumper cable to go from the internal 3-pin connector
to the 3-pin ultrafine connector on the Dixie.

This is utterly unrelated to the comparator functionality.
