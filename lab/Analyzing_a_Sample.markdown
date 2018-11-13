# Analysing a Sample

## Looking at Malware Sample Reports

We're going to skip the actual "threat hunting" and jump straight to looking at a sample report. 

Go to the report [here](https://www.hybrid-analysis.com/sample/5c40eb12fa12d2c3b34ab0ee194d4f42a14cf24dbd4d165571efcb18d2193cbc?environmentId=200) and note the various headlines within the report: 

- Risk Assessment
- Sandbox Artifacts
- Malicious Indicators
- Suspicious Indicators
- Informative
- File details
- File Permissions
- File Activities
- File Receivers
- Extracted Strings

We can actually get a _lot_ of data about a sample just from this report, without even needing to reverse the .apk file!

**★Scroll down to *File Details*, and switch the *All Details* toggle to "ON".**

Now we can see even more details about the sample! 

### Details About TelegraamX.apk 

**SHA256:** `5c40eb12fa12d2c3b34ab0ee194d4f42a14cf24dbd4d165571efcb18d2193cbc`

[Details about SHA256]

**Package Name:** `com.telegram.telegram4x`

The package name ...

**Entrypoint:** `com.telegram.telegram4xorg.telegram.ui.LaunchActivity`

This detail will come in handy for us later when we start reversing the application. It tells us which activity is responsible for the initial functionality of the application. It's the first place you should look when reversing the app.

### File Permissions

Sometimes file permissions can be misleading: certain apps can request _way_ too many user permissions without actually doing anything malicious with them. 

However, they tend to still be great indicators of malicious activity for most applications. 

In this example, we see:

[ Image of permissions ]

along with a number of other permission requests. Those highlighted in "red" (pink. Salmon?) are the most potentially dangerous. We can see that the ability to write external storage, access the camera, read/send SMS messages and phone calls, are all considered particularly dangerous.

### Strings

Strings are also a great resource for determining an app's potential for malicious behaviour. Often, malware authors get pretty generous with their logging! They'll include logs for "hiding notifications" or "upload SMS", just to name a few. Scroll through the **Extracted Strings** displayed under the *Interesting* tab, and make note of any you think seem particularly useful.

#### Command & Control Servers

[ What are they ]

Command & Control Servers (aka. C2 servers) are responsible for sending and receiving information from the application. Often these servers contain API endpoints for things like "upload contacts" or "get SMS messages". 

It's usually a good idea to search strings for those formatted like a URL (http | https: | .com | etc.) Sometimes these strings will be base64 encoded, as well. If you find a Base64-encoded string like:

`aHR0cHM6Ly93d3cuc3B5aHVtYW4uY29tL3YxL2ZpbGVVcGxvYWQ=`

In order to decode this, we can use the terminal:

`echo "aHR0cHM6Ly93d3cuc3B5aHVtYW4uY29tL3YxL2ZpbGVVcGxvYWQ=" | base64 -D`

This will give us, 

`https://www.spyhuman.com/v1/fileUpload`

Keep this in mind when reviewing extracting strings from a sample! It's an easy way to malware authors to *sort of* obfuscate their code, without really requiring too much effort on their part.



