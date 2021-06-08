# Notes for MITx 6.00.1x Introduction to Computer Science and Programming Using Python

This repository contains my notes for the MITx 6.00.1x program, that I am attending during June'21 - August'21. Notes are in markdown format. These can be built into a PDF using pandoc.

## Contributing & Pull Requests

You can contribute by writing chapters, proofreading existiting chapters, adding more examples, rewriting sections etc. Please read CONTRIBUTING.md to know more.

## About The Template

The current template based on [wikiti/pandoc-book-template](https://github.com/wikiti/pandoc-book-template).

## Issues

If you happen to find any errors, please bring it to my notice so that it can be fixed.

## Build

While this project is incomplete, I will not be regularly providing PDFs. It is easy to generate a PDF yourself.

### Dependencies

You need `pandoc` and basic Tex/LaTeX tools present on your system. On Arch Linux, you can install them via this command

```sh
sudo pacman -S texlive-latexextra pandoc
```

Other required packages will be pulled in as dependencies.

If using a different distro, you will probably be able to find these packages in the repos.

In addition, this project uses `make` as a build utility.

### Building PDF

Assuming you have the required dependencies, the following should be run at project root and it will place a PDF in `build/pdf/book.pdf`.

```sh
make pdf
```

## License

 <p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/flyingcakes85/MITx-6.00.1x-Notes">Notes for MITx 6.00.1x Introduction to Computer Science and Programming Using Python</a> by <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://github.com/flyingcakes85/">Snehit Sah</a> is licensed under <a href="http://creativecommons.org/licenses/by-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">CC BY-SA 4.0<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1"></a></p>
