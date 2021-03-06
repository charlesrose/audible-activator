# audible-activator

A script to retrieve your activation data (activation_bytes) from Audible
servers.

## Usage

```
$ ./audible-activator.py -h
Usage: audible-activator.py [options]

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -d, --debug           run program in debug mode, enable this for 2FA enabled
                        accounts or for authentication debugging
  -l LANG, --lang=LANG  us (default) / de / fr
  -p PLAYER_ID          Player ID in hex (optional)

$ ./audible-activator.py
<enter username and password>

$ ./audible-activator.py -l de  # for "de" users
<enter username and password>

$ mpv --demuxer-lavf-o=activation_bytes=CAFED00D sample.aax

$ ffplay -activation_bytes CAFED00D sample.aax
```

## Quick Setup

Python 2 is required along with Selenium and ChromeDriver.

```
pip install requests  # use "easy_install" if pip is missing

pip install selenium

Download and extract the correct zip file from the https://sites.google.com/a/chromium.org/chromedriver/downloads site to this folder.

```

Ryan reports that the 32-bit Mac ChromeDriver works fine under a 64-bit Mac
environment.

## Anti-Piracy Notice

Note that this project does NOT 'crack' the DRM. It simplys allows the user to
use their own encryption key (fetched from Audible servers) to decrypt the
audiobook in the same manner that the official audiobook playing software does.

Please only use this application for gaining full access to your own audiobooks
for archiving/converson/convenience. DeDRMed audiobooks should not be uploaded
to open servers, torrents, or other methods of mass distribution. No help will
be given to people doing such things. Authors, retailers, and publishers all
need to make a living, so that they can continue to produce audiobooks for us to
hear, and enjoy. Don’t be a parasite.

This blurb is borrowed from the https://apprenticealf.wordpress.com/ page.

## Debugging

If you see an error message like "audible_error=Internal service error has
occured while processing the request, please contact service admin" during the
activation process, then contact Audible customer care and they will clear up
your activation slots (there are 8 such slots).

If you see an "activation loop" in the official software (e.g. Audible Download
Manager), then you are seeing the same exact problem (you activation slots are
all used).

```
$ ffprobe test.aax  # extract SHA1 checksum
...
...
[mov,mp4,m4a,3gp,3g2,mj2 @ 0x1dde580] [aax] file checksum == 999a6a...
[mov,mp4,m4a,3gp,3g2,mj2 @ 0x1dde580] [aax] activation_bytes option is missing!
```

...

Too many authentication attempts result in a temporary 30 minutes ban!

...

$ ./audible-activator.py -d  # run the program in debugging mode

This program is pretty short and easy to debug. I cannot provide end-user
support but I would be very happy to accept patches.

If this program does not work for you and all the debugging steps fail, then
use the https://github.com/inAudible-NG/tables project to recover your
"activation_bytes" in an offline manner.

The good news is that you need to retrieve your "activation_bytes" only once.

...

If you have an Audible username (not an email address), please help in testing
and fixing this program.

### AudibleActivation.sys

It is possible to extract the "activation_bytes" from an existing
'AudibleActivation.sys' file.

```
$ ./AAS-parser.py AudibleActivation.sys
CAFED00D
```

You can grab the 'AudibleActivation.sys' file from various already-activated
devices like Android phones, and Sansa music players.

### Notes

``xhost local:root``


## Credits

* sfgasdfsafggfgg (spindoctors_mix <none@none.com>)

* kidburglar

* Jason Peper (jasontrublu, for "de" support and cleaner code)
