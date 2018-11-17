# Static Analysis on Android Malware

Let's start reversing an actual sample.

#### Grab the malware sample we've looked at from this repo [here](). 

What kind of file is it? Try to figure out how to "unpack" it. 

`$ file 5c40eb12fa12d2c3b34ab0ee194d4f42a14cf24dbd4d165571efcb18d2193cbc_2TbMzN6Erj.bin.gz`

Once you've unzipped it, _now_ see what kind of file it is. What happens if you "unpack" it again!?

#### Rename `5c40eb12fa12d2c3b34ab0ee194d4f42a14cf24dbd4d165571efcb18d2193cbc_2TbMzN6Erj.bin` to `5c40eb12fa12d2c3b34ab0ee194d4f42a14cf24dbd4d165571efcb18d2193cbc_2TbMzN6Erj.apk`.

You've likely seen that unzipping the ".bin" file actually gives you an unzipped `.apk` package! So we can just rename the `.bin` to `.apk` and continue our reversing.

#### Using **APKTool**, decompile the `.apk`.

`$ apktool d 5c40eb12fa12d2c3b34ab0ee194d4f42a14cf24dbd4d165571efcb18d2193cbc_2TbMzN6Erj.apk -o malware_folder` 

The `-o` here allows us to specify the output location of the decompiled files!

#### What interesting elements does the sample contain? 

Look for strings. Run `strings` on the `classes.dex` and `classes2.dex` and note any potentially interesting results! Also check out the Resources and Assets folders. Do you see anything interesting in there?

#### Open your `.jar` files in JD-GUI. Navigate to `AndroidManifest.xml`.

The "Manifest" will give us a significant amount of useful information about the sample we're analyzing. 
What permissions stand out to you? Are there any that we didn't see in the report?

For example, `<uses-permission android:name="com.android.launcher.permission.UNINSTALL_SHORTCUT" />`

Now, look at this line,

```
<activity android:configChanges="0x4b0" android:hardwareAccelerated="@bool/useHardwareAcceleration" android:launchMode="2" android:name="org.telegram.ui.LaunchActivity" android:theme="@style/Theme.AppCompat.Light.NoActionBar" android:windowSoftInputMode="0x20">
      <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
        <category android:name="android.intent.category.MULTIWINDOW_LAUNCHER" />
      </intent-filter>
      
      ...
```

Now let's poke around at the malware's classes.

#### Create an executable `.jar` with Dex2Jar for `classes.dex`. 

	1.	In the root `Dex2Jar` directory run: `./gradlew distZip`
	2.	`cd dex-tools/build/distributions`
	3.	Unzip the file `dex-tools-2.1-SNAPSHOT.zip` (file size should be ~5 MB)
	4.	Run `d2j-dex2jar.sh` from the unzipped directory
  
  `$ sh d2j-dex2jar.sh classes.dex`
  
#### Repeat with `classes2.dex`

#### Open the .jar files in JD-GUI.

What is the first activity that's launched? What is it doing?

#### Find malicious activity.

Many times, malware authors embed malicious code in benign applications (like this one). How can you figure out which code is malicious, and which isn't? Think back to one of the permissions we saw! 

#### Search for other IOCs. List them! 

We'll continue looking at malicious classes together. But, there are a _ton_ of other ways to analyze malware that we didn't have time to cover today. Behavioural analysis, dynamic analysis -- these are also great ways to better understand what a malicious application may be doing! 

### Check out the next page for a list of resources for continued learning :) [NEXT](https://github.com/chmodxx/BlackHoodie2018/blob/master/lab/Resources_and_Learning.markdown)
