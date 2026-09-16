# Samsung Galaxy S6 Mobile Forensics — NIST Case Study

A hands-on digital forensic investigation of a **Samsung Galaxy S6 (SM-G920A)** physical extraction based on the **NIST Mobile Forensics Black-Box Study**.

The investigation focuses on recovering, examining, and documenting artifacts from the provided Android physical image using **Autopsy** and manual forensic analysis.



## 📌 Case Overview

This project analyzes a forensic image obtained from the NIST mobile forensic case scenario.

The investigation was conducted as an artifact-driven examination rather than simply answering the case questions. Recovered artifacts were examined and correlated across different parts of the Android filesystem to understand the activity associated with the device.

### Device

| Attribute | Details |
|---|---|
| Device | Samsung Galaxy S6 |
| Model | SM-G920A |
| Acquisition | UFED Physical Extraction |
| Evidence Image | `blk0_sda.bin` |
| Analysis Tool | Autopsy |
| Case Source | NIST Mobile Forensics |



## 🎯 Objectives

The primary objectives of this investigation were to:

- Examine the Android physical image and filesystem structure.
- Verify the integrity of the acquired evidence.
- Identify system and user-related artifacts.
- Recover communication and contact artifacts.
- Examine browser and search history.
- Analyze Tor-related artifacts.
- Recover geolocation information from media.
- Examine Wi-Fi configuration artifacts.
- Investigate Bluetooth pairing and vehicle-related artifacts.
- Examine Google Drive application artifacts.
- Correlate artifacts across applications and system locations.
- Document forensic findings and extraction limitations.



## 🧪 Evidence Integrity

The original acquisition archive was obtained from the **NIST Mobile Forensics Black-Box Study**.

The physical image extracted from the acquisition was:

```text
blk0_sda.bin
````

### SHA-256

```text
7B5EF155A6E07AD4D5C67FAA65F715552CDB4D5CDA2E8C45B8104E0F63A84EB4
```

The hash was calculated from the physical image and compared with the acquisition metadata.

> **Note:** The original forensic image is not stored in this GitHub repository because GitHub's normal Git storage has a 100 MB per-file limit. The original NIST evidence should be obtained from the authoritative NIST source.

### Original NIST Evidence

The original evidence file is:

```text
UFED_Samsung_GSM_SM-G920A_Galaxy_S6_2019_08_13_(001).zip
```

**NIST source:**
[https://s3.amazonaws.com/docs.nsrl.nist.gov/de_blackbox_study/mobile_test/UFED_Samsung_GSM_SM-G920A_Galaxy_S6_2019_08_13_(001).zip](https://s3.amazonaws.com/docs.nsrl.nist.gov/de_blackbox_study/mobile_test/UFED_Samsung_GSM_SM-G920A_Galaxy_S6_2019_08_13_%28001%29.zip)

The SHA-256 value above can be used to verify the integrity of the physical image used during analysis.



# 🔍 Investigation

The examination was performed in an artifact-centric workflow.

## 1. Evidence Identification and Filesystem Examination

The UFED physical extraction was examined and the Android filesystem was identified in Autopsy.

The physical image was loaded as a raw image and the filesystem was examined through the recovered volume structure.



## 2. System and User Artifacts

### User Account

The Android user configuration contained:

```text
jd tester
```

Recovered from:

```text
/data/system/users/0.xml
```

### Device Time Zone

The device contained:

```text
America/New_York
```

Recovered from:

```text
/data/property/persist.sys.timezone
```

### Pattern Lock Artifact

The Android gesture pattern hash was recovered from:

```text
/data/system/gesture.key
```

This file contained a 20-byte binary value associated with the device's pattern-lock artifact.



## 3. Geolocation and Image Metadata

The image:

```text
20190809_120201.jpg
```

contained EXIF metadata including GPS coordinates.

Recovered coordinates:

```text
Latitude:  36.15055555555556
Longitude: -95.94777777777779
```

The coordinates correspond to:

```text
Tulsa, Oklahoma, USA
```

The image metadata also contained the device information:

```text
Samsung SM-G920A
```



## 4. Wi-Fi Artifacts

Wi-Fi configuration artifacts were examined to identify previously recorded wireless access points.

A total of:

```text
8
```

distinct Wi-Fi access-point configuration entries were identified in the examined artifact.



## 5. Communication Artifacts

WhatsApp artifacts were examined through the recovered application database.

The investigation identified communication associated with a potentially illegal transaction.

A phone number associated with the device was recovered as:

```text
9182360870
```

WhatsApp location-sharing artifacts were also identified, including a location attachment associated with communication concerning a meeting location.



## 6. Browser and Search Activity

Chrome browser artifacts were examined from:

```text
/data/com.android.chrome/app_chrome/Default
```

Search activity included queries related to:

* firearm prices
* drug prices
* heroin
* black-market pricing
* Orlando Springs Park

These artifacts were used to establish the nature of the searches performed on the device.



## 7. Tor Browser Artifacts

Tor-related artifacts were recovered from:

```text
/data/org.torproject.torbrowser/app_torservice/.tor/state
```

The state file contained:

```text
LastWritten 2019-08-09 14:55:23
```

The artifact therefore records Tor service state activity at approximately:

```text
09 August 2019 — 2:55 PM
```

A Tor-related browser artifact also contained the clearnet domain:

```text
www.deepwebsiteslinks.com
```

along with an associated `.onion` address.



## 8. Bluetooth and Vehicle Artifacts

Bluetooth configuration and pairing artifacts were examined.

The local phone Bluetooth adapter was identified as:

```text
3c:bb:fd:6a:00:32
```

The investigation also identified a paired **Uconnect** device:

```text
Name:
Uconnect 1C4RDHAG7HC690071
```

Bluetooth address:

```text
00:54:AF:68:D4:F4
```

The Bluetooth address corresponds to the recovered pairing artifact.

> **Important:** The string `1C4RDHAG7HC690071` was recovered within the Bluetooth device name. It is not independently treated as a validated VIN without additional corroborating evidence.



## 9. Google Drive Artifacts

Google Drive application data was examined from:

```text
/data/com.google.android.apps.docs/app_cello/jd.cvult@gmail.com
```

The associated Google account was:

```text
jd.cvult@gmail.com
```

The `cello.db` database contained entries including:

```text
My Drive
Getting started
```

Google Drive application configuration also contained download-related functionality.

However:

> The presence of download-enabled configuration does **not by itself prove that the user downloaded a particular document**. An actual download would require supporting file or activity evidence.



# 🛠️ Tools Used

* **Autopsy**
* Manual filesystem examination
* Android artifact analysis
* SQLite database examination
* EXIF metadata analysis
* Browser history analysis
* Bluetooth artifact analysis
* Tor artifact analysis
* Hash verification



# 📄 Report

The complete forensic investigation report is available in:

```text
NIST_Galaxy_S6_Forensic_Artifact_Report.docx
```

The report documents:

* Evidence integrity
* Filesystem examination
* Recovered artifacts
* Artifact paths
* Browser activity
* Communication artifacts
* Geolocation
* Tor artifacts
* Bluetooth artifacts
* Google Drive artifacts
* Extraction and parsing limitations
* Consolidated findings



# ⚠️ Forensic Limitations

Some automated forensic parsing tools did not successfully recover all expected artifacts from the image.

Therefore, the investigation relied substantially on:

* Autopsy filesystem examination
* Direct artifact inspection
* SQLite database examination
* Manual correlation of recovered evidence

A failure of an automated parser to produce an artifact was **not automatically interpreted as evidence that the artifact did not exist**.

Similarly, parser limitations were not treated as proof that the original UFED acquisition itself was corrupted.



# 📚 Case Reference

This investigation is based on the NIST:

**Results from a Black-Box Study for Digital Forensic Examiners**

National Institute of Standards and Technology (NIST).

The original NIST case material should be consulted for the official scenario, evidence acquisition information, and examination questions.



# ⚖️ Disclaimer

This repository is intended for:

* Digital forensics education
* DFIR training
* Academic research
* Forensic tool practice
* Reproducible artifact analysis

The investigation documents findings recovered from the provided NIST case image. Interpretations are limited to the artifacts examined and should not be treated as conclusions about real-world individuals outside the context of the NIST test scenario. I have investigated this case solely for my practice purpose.

---

## 👩‍💻 Author

**Lakshita Soni**

Cybersecurity | Digital Forensics | Malware Analysis


