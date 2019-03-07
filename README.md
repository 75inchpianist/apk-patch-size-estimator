# APK patch size estimator
Estimates the size of Google Play patches and the new gzipped APK.

From two APKs it estimates the size of the new patches as well as the size of the gzipped version of the new APK, which would be used in
cases where the patches are unexpectedly large, unavailable, or unsuitable.
Google Play uses multiple techniques to generate patches and generally picks the best match for the device. The best match is usually, but not always, the smallest patch file produced. The numbers that this script produces are **ESTIMATES** that can be used to characterize the impact of arbitrary changes to APKs. There is **NO GUARANTEE** that this tool produces the same patches or patch sizes that Google Play generates, stores or transmits, and the actual implementation within Google Play may change at any time, without notice.

***This is not an official Google product***

## Usage

The script uses *Python 2.7.X*, *bsdiff* and *Java* (you may need to install them in your system)

For the file-by-file estimation we use a jar (at /lib/file-by-file-tools.jar) generated from: https://github.com/andrewhayden/archive-patcher

#### To estimate the patches sizes of two APKs run:
```bash
$ python apk_patch_size_estimator.py --old-file old.apk --new-file new.apk
```

#### Output:
```bash
               None           GZIP           BROTLI
None           6.54MB         6.54MB         6.54MB
BSDIFF         6.54MB         2.12MB         2.12MB
File-By-File   6.54MB         2.12MB         2.12MB
```

## Patches estimation process

### Bsdiff estimation
![](images/apk_patch_size_estimator.png) 

### File-by-file estimation
Please visit https://github.com/google/archive-patcher for further details.

## Installing external dependencies
The script uses *bsdiff*, *gzip*, "brotli", *head*, *tail*, *bunzip2* and *java* binaries, [**bsdiff**](https://www.freebsd.org/cgi/man.cgi?query=bsdiff) and [**brotli**](https://github.com/google/brotli) are the only ones not installed by defult in a unix based OS.

#### Linux debian-based
Install bsdiff:
```bash
sudo apt-get install bsdiff brotli
```

#### OS X
Install bsdiff using [Homebrew](http://brew.sh/):
```bash
brew install bsdiff brotli
```

#### Windows

The easiest way to run the script in Windows is by using [Cygwin](https://www.cygwin.com/), make sure you install *python* and *bsdiff* using Cygwin's installer/setup.

## Runing the unittests

#### Install unittest.mock 
```bash
pip install mock
```

#### Run the test
```bash
python -m unittest discover tests/
```

## Authors
    Julian Toledo
    Andrew Hayden
    Song Pan
