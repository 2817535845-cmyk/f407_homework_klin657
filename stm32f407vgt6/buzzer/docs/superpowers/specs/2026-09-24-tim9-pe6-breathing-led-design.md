# TIM9/PE6 breathing LED design

## Goal

Drive the M100Z-M4 board's green user LED (LED1) with a hardware PWM breathing effect.

## Hardware mapping

- MCU: STM32F407VGT6
- LED1: PE6, active low (the MCU sinks current to illuminate it)
- Timer channel: TIM9_CH2 on PE6, alternate function AF3

## Configuration

- TIM9 uses the APB2 timer clock (168 MHz with the existing clock tree).
- Prescaler: 167; period: 999; PWM frequency: 1 kHz.
- PWM mode: PWM 1; output polarity: low; initial pulse: 0.

## Source changes

1. Replace the TIM4/PD13 configuration in `board.ioc` with TIM9 Channel 2 PWM on PE6.
2. Regenerate CubeMX code so that `tim.c` and `tim.h` define `htim9` and `MX_TIM9_Init`.
3. Update `main.c` to start TIM9 Channel 2 and vary CCR2 from 0 to 1000 and back.
4. Build the `Debug` preset and verify `board.elf` is produced.

## Success criteria

- The generated project compiles with no errors.
- After flashing and running, the green LED on PE6 smoothly brightens and dims over about four seconds.
