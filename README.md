# fansyloader - The fancy loader

Fansyloader tries to solve the problem that it seems to be difficult for most people to install the Python interpreter or use Github.
For this Fansyloader allows you to download your content from Onlyfans and Fansly easily and quickly, 
without reading long installation instructions or making complicated configurations.

## Using

1. Download the [last released version](https://github.com/montroly/fansyloader/releases)
2. Unpack the download
3. Open a bash and navigate to the directory. (For Windows the use of the Powershell is recommended and the script `openshell.bat` is optional included to open the Powershell). 
4. (Optional) `./fansyloader setup`
5. Start

  ```bash
  ./fansyloader
  ```

**Credits:** This project would not have been possible without the work of @hippothon, @OFfriend and @DIGITALCRIMINAL (±S).
They cleared many barriers during their work on [OnlyFans DataScraper](https://github.com/DIGITALCRIMINALS/OnlyFans).

## Configuration

Fansyloader creates a configuration directory at first startup, which contains a configuration file `config/config.toml`. 
This file can be opened and modified with a text editor and contains an explanation for most parameters.

More information can be [found here](./conf.md)

## Troubleshooting

After the download is started, only the progress bars and no error messages are displayed. 
So if there are problems, you should look into the log file in the `config` directory. 
Alternatively, `show_progress_bar` can be set to `false` in the configuration file.

More information can be found in the [FAQ](./FAQ.md).
If you can't find a solution to your problem, open an issue and pay attention to [how to share data safely](secure_share.md).

## Enjoy what you see? 

Give me a tip:

```text
BTC bc1qtwpc4pr4qzmf0e0a74pp9v22pee0ltmx0tv2v5
ETH 0xceAFb01aF935b781724954314597542fFd6B3Ff9
XMR 44mvKqQAJYm4xgfAgyjguUiTRGtAXp1Uz1giQoHyTASRWyMDMVzwWRkCAu9AynQhBAUmdVoUfMqyWVykQ5i9bgFL27tgT8Z
```

## Disclaimer

The contributors to this software are not responsible for what their users do with it or how they use it.

