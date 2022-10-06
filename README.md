# Digital Undersökningsteknik

--- 

## The Three A:s (proof requirements)

The basic methodology consists of the 3 As:
- **Acquire** - without change or damage
- **Authenticate** - trustworthy 
- **Analyze**

---

## Forensic Image 
>A Forensic Image is a bit-by-bit / sector-by-sector direct copy of a physical storage which copies all files and folders and unallocated space, slace space, and free space. A Forensic Image is also called a **Complete Copy** 

>Always create a **super copy** (copy of a copy) when working with a disk.


### Raw/dd
- Contains no MetaData, error correction, or piecewise hashing.
- No error correction.
- The whole disk copy on one file.
- Command line tool.
- Tool may destroy source media if used incorrectly.
- Can be used by standard linux tools

### EWF(Expert Witness Disk) E01 (Encase Image File Format)
- Uses compression (Smaller Image size)
- Includes metadata
- Keeps backup of various types of acquried digital evidence that includes disk imaging
- When creating backup of available data, a physical bit stream is created
- Divides the data into data chunks (often 640mb)
- Has built in checksumming **CRC**(**Cyclic Redundancy Check**) CRC is an error – detection code used by the Encase in E01 files to check for any accidental changes in the original data. 
- Do not work with all Drives e.g., DVDDrive
  [SOURCE](https://www.forensicsware.com/blog/e01-file-format.html)
- Requires 3rd party tools to be handled. 
 
---

## Recreation of Files
>A file can be recreated through different ways. Here is some methods  mention of possible ways to recover files:

#### MS-Windows, NTFS
- Windows BackUp system
- MetaData $MFT Records
- Memory 
- Carving (Searching in unallocated space for deleted files) Some part can still exists if it has not been overwritten

#### Linux, FAT, exFAT
**One Way**
debug the filesystem to find the files Inode. With the Inode information run dd command to recover the file.

---

### MetaData in a File 
>Data about data. Can be things like when a document has been modified, created, viewed, etc. There are files like .lnk and .spl that contain metadata.

There are a file such as **.lnk**(Windows shortcut)  that contain metadata.

#### Thumbs.db

Används generellt i Windows. Finns många olika versioner av filen. Filen underlättar för användaren. Sparar förhandsgranskning (thumbnails) för filer i varje mapp. Bilder i Thumbs.db försvinner kanske inte när bilden i sig tas bort. I nyare versioner finns filer i %Application data%/Explorer/.

#### MetaData in Word-Document
- Title 
- Author
- Subject and keywords
- Timestamps **MAC**, - Modified, Accessed, Created
- Tracked changes 
- Statistics

#### MetaData Digital Image  (.jpg)
**EXIF-TAGS**
- Timestamps **MAC**, - Modified, Accessed, Created
- FileInfo - Name, Size, Type, Width, Height
- GPS information (possible)
- Lens Information - type of camera, e.g., Iphone 12 dual wide..
- FLASH

#### MetaData SmartPhones
- Identification of a cellular network tower (BTS), time a phone call/SMS were made. 
- geo-Locations of phone
- Extracted userData such as - Messages, Web History, retrived/sent email, history, dictionary, etc.
- Pictures - GEO-Tags and mentiond metadata from pictures. *See Above* INFO
---
## Methods
>There are different types of methods used for collecting evidence.  All methods use the same Procedure

### Procedure / Forensic Investigation
1.  **Collection** - Discover, Indentify and document every useful evidence.
2.  **Preservation** - Creation of Forensic Digital Copy (Authenticated) Hashsum
3.  **Recover** - Restore wastebin Folder
4.  **Carving** - Search for erased file in unalloctaded space, mutliple versions can be found when saved a new copy is created. Only erased the pointer that points to the data block that contains the file.
5.  **Reduction** - remove unrelated files, e.g., Operating System files. Run a comparison against databse of operating system files hashsum
6.  **Harvesting** - gather the data you looking for. Autopsy
7.  **Formulating Hypothesis** - Create Hypothesis from gathered material.
8.  **Analysis** - Temporal/Time, relation, functional
9.  **Reconstruction** - Summarize the results gathered and combine tall into one. 
10. **Investigation report** - Creation of report about findings. Everyone should understand.
11. **Testimony in court** - State all you did, can be long time between investigation and court

CPRCRHFARIT

### Live Forensic
> Live Forensic means analysis of a running system. Very important for securing volatile evidence such as running processor, network connections, system time, logged in users, command history, Memory Analysis, etc.

### Static Forensic
>By Static Forensic is meant analysis of a system or component at rest - such as a hard drive. Here you can extract non-volatile data such as files, parts of the registry, email, swap files, use USB devices, etc.

**OBS** Just shut down the power. Dont shut down computer. Then it will empty all files from temp etc


### Network Forensic
>By Network Forensic is meant analysis of networks. Usually this consists of monitored data in a network where you can find which devices are communicating with each other and what data they are sending. You can find which devices belong to an IP address, which pages are visited, etc.

- WireShark - xxx.pcap files 
- NetworkMiner

### Cloud Forensic
There are several dimensions to the problem. Partly legal problems - you can get access to a World Cup by decision, but how to proceed when analyzing the cough? If you dump memory, you get access to all guests on the system, which is not desirable.

Another problem can be large networks where there are many VMs used in a service. They look the same and work the same way. If one is hacked, how does one perform an analysis? Which physical machine is running the virtual machine? Hard to know where things are going.

When working with the WC, you can take a snapshot and clone the WC. You can redo the disk and work with it using traditional tools.

After the GDPR, some have implemented "One Button Take Out" which means that a company can easily provide a cloud service such as IBM.

Furthermore, certain services are run as containers.
[SOURCE](https://github.com/CourseNotesBTH/DV1592/blob/master/Cheat%20Sheet.md)

---

## USB - Forensic
From the use of a USB-drive you look for:
- when a USB drive was connected to a system
- when it was disconnected
- how long the USB flash drive was connected to a system
- typ of USB
- serial number.

**EventViewer** | **Registry**
 - Vendor, Product, Version 

\System\MountedDevices - Determine Mounted Letter For USB. 

**Shellbags** - Settings for folders, saved in shellbags. Can see what was in USB if exlorer windowd was edit.

---

### Chain Of Custody
> A process that tracks the movement of evidence through its collection, safeguarding, and analysis lifecycle by documenting each person who handled the evidence, the date/time it was collected or transferred, and the purpose for the transfer. [SOURCE](https://csrc.nist.gov/glossary/term/chain_of_custody)

> The chain of custody requires that from the moment the evidence is collected, every transfer of evidence from person to person be documented and that it be provable that nobody else could have accessed that evidence. It is best to keep the number of transfers as low as possible.

### Chain Of Evidence
> A process and record that shows who obtained the evidence; where and when the evidence was obtained; who secured the evidence; and who had control or possession of the evidence. The “sequencing” of the chain of evidence follows this order: collection and identification; analysis; storage; preservation; presentation in court; return to owner.

The Connection between Evidence 

---

## (MO) Modus Operandi
> Form of behavior analysis.

Approach / behavior - how a perpetrator acts.

Can consist of how people express themselves, what methods they use and how they intend to make money.

- The perpetrator
- Motive
	- Material
	- Emotionally
	- Psychologically
- Methods
- Behavior

---
## Logs

#### Event Logs MS-Windows
Can be viewed with **EventViewer.exe** and logs are stored at `windows/System32/winevt/logs`
- Application Log
- System Log
- Security log
- Setup Log

#### Linux Logs 

---
## MS-Windows Registry
Standard hives and their supported files. 
files are stored at `Windows\System32\Config\` & NTUSER.dat is stored at: ` C:%windows%\Profiles%user%.`
- HKEY_CURRENT_CONFIG - System
- HKEY_CURRENT_USER - NTUSER.dat
- HKEY_LOCAL_MACHINE
  - Security
  - Software
  - System
- HKEY_USERS_DEFAULT - Default


---
## Filesystems
>File system task is to store data. Different operating systems have different approaches and save different metadata. Most file systems have a hierarchical principle. Others have graphs or streams. You usually have methods for creating, reading, modifying, deleting and moving data.

#### NTFS
>Windows filesystem

#### FAT12, FAT16, FAT32, exFAT

#### APFS (Apple File System) 

#### EXT2, EXT3, EXT4, UFS, ZFS 
---
### Rapport Writing
Three key points

- Objectivity / no criminal classification
- Easy to understand / adapted to the reader
- Detailed analysis, but still relevant

It is not a "thesis" - it is short and concise.

- Sammanfattning
- Innehållsförteckning
- Inledning
- Beskrivning Material
- Iakttagelser och undersökningar
- Analys och slutsats
---
## Analysis
>Different forms of analysis

#### Time/Temporal Analysis
Analyzing time to create structured view of events. Create a timeline 

#### Relations Analysis
Determine where a person or an object was in relation, which computer a suspect was using. Other relations from social media. Create a **Sociogram**
which means to collect information from social netowrks to connect friends hobbys, chatting history etc. 
#### Function Analysis
Kan det här verkligen ha hänt
— Under så kort tid så stora datamängder 
— Realistiska värde

#### Motive Analysis
---
## RAID
>Redundant Array of Inexpensive Disks / Redundant Array of Independet Disks. Connect several disks for better performance

#### RAID 0
Striped. disks put together for one bigger disk.

#### RAID 1
Mirroring. used for redundancy, two disks contain the same data.

#### RAID 0+1
Uses four disks. Two pairs of redundant disks.

---
## Steganografi - Data Hiding
Steganos - Hidden/Covered writing

#### ADS Alternative data stream

"a file inside another file"
[Showcase of ADS](https://blog.foldersecurityviewer.com/ntfs-alternate-data-streams-the-good-and-the-bad/)

**Place a calc after a file**
```powershell
type c:\windows\system32\calc.exe > file1.txt:calc.exe

start c:\file1.txt:calc.exe
```

#### HPA(Host Protected Area)
>HPA is a hidden partion that is normally used to hide a factory installastion op operating system. This Area can be used to hide a partion or make an invisible one. 

---
#### Write-Blocker
>A forensic disk controller or hardware write-block device is a specialized type of computer hard disk controller made for the purpose of gaining read-only access to computer hard drives without the risk of damaging the drive's contents. [SOURCE](https://en.wikipedia.org/wiki/Forensic_disk_controller)
---
### SSD - TRIM
Trim was introduced in Windows 7. 

>A trim command enables an operating system to inform a solid state device which blocks of data are no longer considered in use and can therefore be deleted internally

Not good for a forensic investigation --> The operating system deletes data if it is not used. Data can then not be recreated from unallocated space on SSD

---
<center> Anton Karlsson <br>
