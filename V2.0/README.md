# FYSETC-ERB

This is dedicated controller board for VORON ERCF

![](images/board1.png)

## Features

1. Base on popular RP2040 chip, cheep,available

2. Power management chip, comparing to LDO chip, less heat, more powerful, more steady

3. USB type-C interface and more extra pins out.

## Hardware

There are schemetic, silk and dwg file in `Hardware` folder.

## Firmware

### Compile options
On your klipper device (usually Raspberry Pi) run the following to create your make configuration:

```shell
cd  ~/klipper
make clean
make menuconfig
```

Select the following menuconfig settings

![makemenuconfig](https://user-images.githubusercontent.com/46523240/250621155-6161226d-e69b-42d0-9d05-fd7bc45cc3c5.png)

And create the firmware files by running the following:

```shell
make
```

### Firmware upload

#### 1.With your windows PC

Step 1: Connect 24V (Power on the board)

Step 2: Connect USB-C cable to your Klipper device (usually Raspberry Pi)

Step 3: Push and hold the BOOTSEL button

Step 4: Push the RST button and hold 0.5 seconds

Step 5: Release the RST button, after 3 seconds, Release the bootsel button

Step 6: `RPI-RP2` folder will show up on your computer, copy your built firmware `klipper.uf2` to the folder.

![](images/upload1.png)

![](images/upload.png)

#### 2. With your Pi 

Thanks for mk-maddin's work:
https://github.com/FYSETC/FYSETC-ERB/issues/2#issuecomment-1618902635

##### Connecting the board and bring it into flash mode

Step 1: Connect 24V (Power on the board)

Step 2: Connect USB-C cable to your Klipper device (usually Raspberry Pi)

Step 3: Push and hold the BOOTSEL button

Step 4: Push the RST button and hold 0.5 seconds

Step 5: Release the RST button, after 3 seconds, Release the bootsel button

Verify your device is in boot mode connected by running the following command:

```shell
lsusb
```

The output should contain an entry looking like 2e8a:0003 Raspberry Pi RP2 Boot
![img](https://user-images.githubusercontent.com/46523240/250623553-0dafeb98-9f59-4f13-b555-679653cd394e.png)

##### Flashing the firmware
Now we do not flash the fimware by directly copying it to the storage, but we flash it using the following command:

```shell
make flash FLASH_DEVICE=2e8a:0003
```

The output looks like the following - IF you are prompted (you might or might not) for a password, enter the password of your current user account.
![img](https://user-images.githubusercontent.com/46523240/250625435-4fdd95cf-b75b-43e0-8edd-82496b844ae6.png)

Now restart your fystec-erb by disconnecting 24V - waiting some seconds and reconnecting 24V again.
You should be able to see it as usual klipper device within 
```shell
ls /dev/serial/by-id
```

### Configuration

See `ercf_hardware.cfg` in this repository `config` folder.

### Known issues

The mark of GPIO24 and GPIO25 is swapped, check the silk file [here](https://github.com/FYSETC/FYSETC-ERB/blob/main/hardware/Silk%20Fixed.pdf).
