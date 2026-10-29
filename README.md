
## How to Run

### 1. Build and Flash

1. Open STM32CubeIDE.
2. Import this repository using `File > Import > Existing Projects into Workspace`.
3. Connect the STM32 B-L475E-IOT01A1 via USB.
4. Build the project (`Ctrl + B`).
5. Click **Debug** to flash the firmware.
6. Press **F8 (Resume)** to run the program.

### 2. Basic: PWM Generation

Connect the STM32 to the ZEROPLUS LAP-C(16128):

| STM32 | Logic Analyzer |
| --- | --- |
| PA5 (D13) | A0 |
| GND | GND |

1. Open ZEROPLUS Logic Cube.
2. Select channel A0 and set the sampling rate to 1 MHz.
3. Start capturing the waveform.
4. Use the A/B cursors to measure the period and HIGH time.

To change the duty cycle, modify this line in `Core/Src/main.c`:

```c
__HAL_TIM_SET_COMPARE(&htim2, TIM_CHANNEL_1, 500);
```

| CCR1 | Duty Cycle |
| --- | --- |
| 250 | 25% |
| 500 | 50% |
| 750 | 75% |

Rebuild and flash the firmware after each change.

### 3. Option 1(a): Input Capture

1. Configure PB4 (D5) as TIM3_CH1 Input Capture.
2. Power off the board and connect **D13 (PA5) to D5 (PB4)** using a jumper wire.
3. Reconnect the board and start Debug.
4. Press F8 to run the program.
5. Open `Window > Show View > Expressions`.
6. Add the following variables:

   - `capture_started`
   - `period_ticks`
   - `measured_frequency`

7. Click **Suspend** to refresh their values.

Expected results for a 1 kHz PWM:

- `capture_started = 1`
- `period_ticks = 1000`
- `measured_frequency = 1000` Hz

Press F8 to resume execution.
