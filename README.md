# Hardnested attack

### Works on
New MiFare Classic and MiFare Plus without AES (Note that AES is disabled by default)

### Attack

1. Collect 2000-4000 nonces with a NFC card reader. The speed in collecting nonces depends on the reader.

2. Analyze the nonces generated in step 1 in order to reduce the key original space of 2^48

3. Offline Brute Force

### Software

Before using other methods, always try to use **mfoc** first, since it's the faster and easiest method, if the card is vulnerable to nested attack

```bash
$ git clone https://github.com/nfc-tools/mfoc
$ cd mfoc
$ autoreconf -vfi
$ ./configure
$ make
$ sudo make install
```

If mfoc shows "Card is not vulnerable to nested attack", you have to use hardnested attack.
You can do this with an automatic tool, or manually

#### Automatic method

```bash
# Installation
$ git clone https://github.com/nfc-tools/miLazyCracker
$ ./miLazyCrackerFreshInstall.sh

# Run with a usb NFC card reader connected
$ miLazyCracker
```

#### Manual method

```bash
# Installation
$ git clone https://github.com/aczid/crypto1_bs
$ cd crypto1_bs
$ make get_craptev1
$ make get_crapto1
$ make
$ sudo make install

# Usage
$ libnfc_crypto1_crack <known_key> <for_block> <A|B> <target_block> <A|B>

# Example
# Note that we have to write the block, not the sector, so the 20th block is the last block of sector 5, and the 24th block is the last block of sector 6
$ libnfc_crypto1_crack 0123456789ab 20 B 24 B

```