# tgotext

This is a (very) simple tool to extract translatable strings from Go template files and return them in POT format. It was written to be used together with the [gotext](https://github.com/leonelquinteros/gotext) package. That one already includes [xgotext](https://github.com/leonelquinteros/gotext/tree/master/cli/xgotext), but it only extracts from Go source files.


## Installation

As for non-standard packages, `tgotext` uses [Cobra](https://github.com/spf13/cobra). To build it, run

```bash
go build ./cmd/tgotext
```


## Usage

Assuming the build went well, `tgotext` currently only has one command: `parse`. It expects the path to a template file as an argument, and offers the `--object` flag to specify the name of the `Locale` object that is referenced in the template. That is, if you named your `Locale` object `Loc` and therefore use like `{{ .Loc.Get "Your text goes here!" }}` or `{{ $.Loc.Get "Your text goes here!" }}` in a template file called `/tmp/my_template.tpl.html`, you would call:

```bash
tgotext parse /tmp/my_template.tpl.html --object .Loc > /tmp/default.pot
# Or for templates using the root context:
tgotext parse /tmp/my_template.tpl.html --object $.Loc > /tmp/default.pot
```

The tool doesn't write files directly, it only prints to `stdout` so you can redirect the output as you like.

There's also a global flag `--header`, if that is added to the call the output will start with a template POT header. You can use it with the first template if there are more than just one, and append the output from the other ones without it:

```bash
tgotext --header parse /tmp/template1.tpl.html --object Loc > /tmp/default.pot
tgotext parse /tmp/template2.tpl.html --object Loc >> /tmp/default.pot
tgotext parse /tmp/template3.tpl.html --object Loc >> /tmp/default.pot
```


## Caveat

I just wrote this thing in like an hour. It worked well with my templates, that's what i needed it for, but i haven't tested it with anything else.


## Contributing

To ask for help, report bugs, suggest feature improvements, or discuss the global development of the package, please use the issue tracker on GitHub.

### Branches

Please note that all development happens in the develop branch. Pull requests against the master branch will be rejected, as it is reserved for the current stable release.


## Licence

Copyright 2023 Meik Michalke meik.michalke@hhu.de

`tgotext` is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

`tgotext` is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with `tgotext`. If not, see https://www.gnu.org/licenses/.
