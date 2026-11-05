# nand_flasher-ai

STM32F4 NAND programmer based on `bubulkabarabylka/nand_flasher`.

## AI revision

This clone keeps the original USB CDC/FSMC/SPI protocol and adds defensive
checks around NAND configuration and address arithmetic:

- rejects invalid HAL and geometry selections before dereferencing function tables;
- rejects overflowing address-plus-length requests;
- validates spare/OOB geometry against the internal page buffer;
- rejects write packets that exceed the active transfer;
- reports NAND read/write failures instead of treating them as successful;
- avoids duplicate entries in the bad-block table.

The firmware remains a raw NAND tool. ECC behavior is still selected by the
host command and should be tested against the target chip before programming.

## Building

The firmware can be built with PlatformIO:

```sh
pio run -e stm32f407_nand
```

Every push to `main` and every pull request runs the same build in GitHub
Actions. Serial monitor settings are intentionally left to the local
PlatformIO configuration rather than being fixed to a particular operating
system port.
