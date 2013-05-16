# packup.sh
packup.sh is a simple script that will take every file in the
current directory, and any subdirectory, and pack them into
a single self-unpacking script. This script can then be
distributed by itself with no other requirements. The user just
simply executes the script and all of the data is unpacked
and all subdirectories are rebuilt. The script is also designed 
to be extensible. A developer can simply source the script
and override any or all of the 4 hook functions.

## Using the script
By default, the script can be used to pack up any number of 
binary or text files into a single self-unpacking bash script.
you can either install the script to a common bin directory
line /usr/bin or $HOME/bin and execute it like any other program, 
or copy it directly to the directory you want to pack up and 
execute it from there

```bash
cp packup.sh /usr/local/bin
chmod +x /usr/local/bin/packup.sh
cd some/directory/to/pack
packup.sh
```

The default output is called output.sh, this can be changed by
using an argument to the script

```bash
packup.sh my_output_script.sh
```

This would create an output script called my_output_script.sh.
Please note that you must be in the directory you want to pack.

## Extending the script
This script is extensible. It has 4 user definable hook functions
that can be overridden. Simply create a new script and source
the packup.sh script. Then override any or all of the 4 user 
functions, user_header(), user_footer(), pre_run(), and post_run().

```bash
#! /usr/bin/env bash

source ./packup.sh

user_header() {
   echo "#Header test" >> "$output"
}

user_footer() {
   echo "#Footer test" >> "$output"
}

pre_run() {
   echo "PRE RUN CODE"
}

post_run() {
   echo "POST RUN CODE"
}

run_pack
```

The user_header(), and user_footer() function get called by the 
packup.sh script and can be used to add new header and footer
data to the output script file to support any custom code in
pre_run() and post_run().

The pre_run(), and post_run() functions are copied to the output
script and run before and after the unpacking process. They are 
not executed by the packup.sh script, only the output script.

you must make sure to call run_pack() at the end of your custom
extension or it won't work. 

## License
This script is available for use under the MIT license.

Copyright (c) 2013 James Slocum (jamesslocum.com)

Permission is hereby granted, free of charge, to any person
obtaining a copy of this software and associated documentation
files (the "Software"), to deal in the Software without
restriction, including without limitation the rights to use,
copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the
Software is furnished to do so, subject to the following
conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES
OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR
OTHER DEALINGS IN THE SOFTWARE.
