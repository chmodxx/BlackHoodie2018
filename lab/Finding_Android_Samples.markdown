# Finding Malicious Samples

It can be difficult to find sophisticated, malicious samples out in the wild. A number of threat-hunting sites and malware repositories are reserved for corporations or graduate students, and free services (like the ones we'll look at today) rely on the community for samples & reports.

Some great resources for malware are [Mila's site](http://contagiominidump.blogspot.com/), and [Hybrid Analysis](https://www.hybrid-analysis.com/). You can also use 3rd party Google Play Store copycat sites for applications that are often removed from Google Play due to malicious activity, but that haven't been removed from 3P stores. [APKPure](https://apkpure.com) is usually my go-to.

We'll be looking at a particular surveillanceware sample that's publicly available. We'll also be reviewing how to find *additional* samples through free services like Hybrid-Analysis.

## A General Android Malware Search

**★ Navigate to *Hybrid-Analysis*:** https://www.hybrid-analysis.com/

In order to take advantage of the search functionality, you *will* have to create an account. (If you don't feel like doing that, you can still do all of the reversing work with the sample you'll download from this repo.)

**★ Sign-up for a free community account**: https://www.hybrid-analysis.com/signup

You will be able to get access to submitted samples, and submit your *own* samples.

**★ Log-In to your new account.**

This is where the fun begins. We're going to look at a general search for malicious Android samples.

**★ Navigate to *"Report Search"***.

Click inside the search bar on the top right-hand corner. You'll see options for YARA Search, String Search and Report Search. Click Report Search.

[ Image 1 ] 

`![Image of Yaktocat](https://octodex.github.com/images/yaktocat.png)`

**★ Specify search criteria.**

We're specifically looking for _Android_ malware. Hybrid Analysis lets us choose what kind of filetype we want, along with some fun filters like: "Uses Technique", "Uses Tactic", whether it has been detected by antivirus softwares, and even the associated domain.

To get an idea of how large the collection of Android malware is on H-A, let's just fill out *Filetype* and *Verdict*.

Set, **Filetype: android** and **Verdict: Malicious**.

[Image 2]

**★ Click "Search Database"**

Android malware tends to be a bit harder to find without a premium account to a site like *Virus Total*. 

## [NEXT](https://github.com/chmodxx/BlackHoodie2018/blob/master/lab/Using_Malware_Reports.markdown)
 
