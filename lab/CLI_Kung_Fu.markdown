# CLI Kung Fu

## Pre-Analysis Tips & Tricks

The command line is your best friend for quickly determining some key information about a malware sample.

### Strings

One of the best places to look for juicy malware hints is in the strings defined by the application. Many times, malware authors won't obfuscate their code or will forget to remove certain logging messages. These can be a great way to figure out what the author is trying to attempt!

`strings classes.dex`

### Base64 Encoded Strings

If you find a Base64-encoded string like:

`aHR0cHM6Ly93d3cuc3B5aHVtYW4uY29tL3YxL2ZpbGVVcGxvYWQ=`

In order to decode this, we can use the terminal:

`echo "aHR0cHM6Ly93d3cuc3B5aHVtYW4uY29tL3YxL2ZpbGVVcGxvYWQ=" | base64 -D`

This will give us, 

`https://www.spyhuman.com/v1/fileUpload`

Many malware authors use Base64 to add _some_ level of obfuscation to their code. 
Keep this in mind when reviewing extracting strings from a sample!

### File Types

As we heard on Friday, malware authors like to also pretend that certain files they're forcing a device to download are non-executable. But! We can check that.

`file <FILE NAME>`

This will tell you what kind of file type you're dealing with & how to either unpack it, or execute it.

### Grep

Grep can be very handy when you're looking for a particular IOC, but don't want to pull out JD-GUI to search for it. 
You may need to install it if you're getting "command not found" errors:

`$ sudo apt-get install grep`

To search for a domain in the resources file, 

`$ grep -C5 "some.sketchy.domain" resources.arsc` This will show 5 lines surrounding any found strings within the file.

You can also "pipe" your strings to grep:

`$ strings classes.dex | grep "http"`

And if it's a large search, you can send _that_ to a file!

`$ strings classes.dex | grep "http" > ~/Desktop/some_found_stuff.txt`




