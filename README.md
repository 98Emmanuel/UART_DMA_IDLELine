UART RX with DMA + IDLE Line
What this project does

This project shows how to receive UART data on an STM32 using DMA with IDLE line detection (HAL_UARTEx_ReceiveToIdle_DMA).

The MCU:

Receives characters over UART using DMA

Detects when the sender stops transmitting (IDLE)

Finds out how many bytes were received

Echoes the received data back over UART using DMA

Restarts reception to wait for the next message

Key points

UART reception is non-blocking

Message length is variable (not fixed)

IDLE line marks the end of a message

DMA reception is explicitly restarted after each message

Half-transfer DMA interrupt is disabled

Interrupts only set flags; all work is done in the main loop

Buffer behavior

A single RX buffer is reused for all messages

The buffer is not protected against overwrite

This is fine for slow, manual terminal input

Not intended for high-speed or production use

What you should see on the terminal

Typing:

12345


Produces:

12345


Exactly once (PuTTY local echo must be OFF).

Why RX is restarted

HAL_UARTEx_ReceiveToIdle_DMA stops DMA when IDLE is detected, even if DMA is set to circular mode.
Therefore, reception must be restarted in software after each message.
