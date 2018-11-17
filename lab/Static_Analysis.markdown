# Static Analysis on Android Malware

Let's start reversing an actual sample.

#### Grab the malware sample we've looked at from this repo [here](). 

#### What kind of file is it? Try to figure out how to "unpack" it.

`$ file 5c40eb12fa12d2c3b34ab0ee194d4f42a14cf24dbd4d165571efcb18d2193cbc_2TbMzN6Erj.bin.gz`

#### Using **APKTool**, decompile the `.apk`.

`$ apktool d 5c40eb12fa12d2c3b34ab0ee194d4f42a14cf24dbd4d165571efcb18d2193cbc_2TbMzN6Erj.apk -o malware_folder` 

The `-o` here allows us to specify the output location of the decompiled files!

#### What interesting strings does the file contain? Run `strings` on the `classes.dex` and `classes2.dex` and look for any potentially interesting results!

#### Create an executable `.jar` with Dex2Jar for `classes.dex`. 

  1.	In the root `Dex2Jar` directory run: `./gradlew distZip`
	2.	`cd dex-tools/build/distributions`
	3.	Unzip the file `dex-tools-2.1-SNAPSHOT.zip` (file size should be ~5 MB)
	4.	Run `d2j-dex2jar.sh` from the unzipped directory
  
  `$ sh d2j-dex2jar.sh classes.dex`
  
#### Repeat with `classes2.dex`

#### Open your `.jar` files in JD-GUI. 

