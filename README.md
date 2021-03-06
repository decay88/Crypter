# Crypter

*Update: Please note that as of December 15th 2017, the direction and purpose of this project has changed due to legal and ethical concerns. Consequently, It's **extremely important** that you read both the **Disclaimer** and **Project Direction Update** sections of this README.*

Welcome to Crypter! a ransomware and builder package written entirely in Python and compiled to a Windows executable using [PyInstaller](http://www.pyinstaller.org/). This README will provide you with all of the information necessary to understand, build and use this software.

**Please note that by making use of this repository you accept and agree with the disclaimer section of this README, as well as the section marked "Project Direction Update".**

Click [here](https://youtu.be/r3jaNHmkkXE) for a video demonstration of Crypter and [here](../../releases) to download the Crypter distributable release, which contains the Crypter repository and all of the required dependencies in a single, convenient package.

 ![Crypter GUI](sample_images/crypter_package.png)
 *Builder application (left) and Crypter ransomware piece (right)*
 
 
 ## Disclaimer - IMPORTANT

*Update: Before reading this section, please also read the section marked "Project Direction Update".*

Crypter is intended for educational and research purposes only. This software should not be used within any system or network for which you do not have permission, nor should it be used for any illegal or illicit purposes. The author takes no responsibility for any damages that may be caused by the software in this repository. 

Once compiled, Crypter WILL encrypt the files on the computer on which it is executed. Whilst Crypter provides you with access to the decryption key (enabling you to decrypt any encrypted files), bugs and other issues could, in theory, interrupt or prevent a successful decryption. 

Consequently, a permanent and irreversible loss of data could occur. To avoid any potential damage, you should only run Crypter on a test machine created for this purpose.

Once again, **the author accepts no responsibility for any damages that may occur, and by downloading this software you accept and agree to this disclaimer, as well as the section marked "Project Direction Update".**

## Project Direction Update
In recent weeks a number of ethical and legal concerns around this project have been raised. Please note that it is **not** my intention to provide criminals with a tool for destructive or harmful purposes. In its current state, Crypter allows users to easily decrypt their files. Once opened, the 256-bit AES key used for encryption is written to a local file in the same directory with the filename **key.txt**. This key can then be used to decrypt all of the encrypted files. It is not hidden from the user, nor is it ever sent to a remote server, Email address etc. In order to truly utilise Crypter for malicious purposes it would likely need to be expanded upon considerably.

Nevertheless, if I continue to develop this project then I may be in risk of breaking local laws by providing a tool that can be used to commit an offense. Consequently, from December 15th 2017 onwards active development of Crypter will cease, and I will no longer be providing direct support.

To clarify exactly what this means, I will fix bugs when highlighted or identified and I may expand upon documentation in the future, but the following will no longer be addressed:
- Development of a remote Command and Control component
- Direct support with regards to feature requests
- Further functionality additions

It's been an interesting and pretty fun journey, but active development on the project should be considered finished from this point onwards.

## Repository Structure
If you're unsure of the components that make up this repository, the following explanation should give you some insight:
```
Crypter
| -- Crypter\ (The actual ransomware code)
| -- build\ (The builder application, configuration and resources used to produce the PyInstaller binary)
  | -- ExeBuilder\ (The Crypter builder package and application)
  | -- Resources\ (Holds resources that are bundled with, and used to build, the Crypter executable)
  | -- builder_gui\ (Contains the wxFormBuilder GUI project, including prototypes, for the Builder)
  | -- Builder.pyw (Launches the builder. Run this script to open the builder application)
  | -- config_example.cfg (An example configuration file that can be loaded into the Builder)
| -- gui\ (The Crypter GUI project files. These can be viewed and edited using wxFormBuilder
| -- sample_images\ (Simply contains sample images used in this README)
```

## Prerequisites
Before cloning the repository and attempting to build Crypter, you must first meet the following prerequisites. You'll then have all the tools required to launch the builder and create the executable.

**Due to the confusion and room-for-error surrounding these dependencies, this repository has been packaged with the additional required software shown in the table below, and can be downloaded as a .zip from the [Releases](../../releases) page.**

**Note:** You should install the software in the exact order shown in the table below, from top to bottom. Without these you wont be able to launch the builder. Errors or issues you may encounter will most likely stem from missing or invalid dependencies.

| Requirement | Supported Versions | Recommended Version |
| ----------- | ------------------ | ----------- |
| Microsoft Windows | 7, 8, 10, Server 2K8 and above | 10 |
| Python | 2.7.13 (x86) | [2.7.13 (x86)](https://www.python.org/downloads/release/python-2713/) |
| Pyinstaller | 3.1.1, 3.2.1 | [3.1.1](https://github.com/pyinstaller/pyinstaller/releases/tag/v3.1.1) |
| Microsoft VC++ for Python | 9.0 | [9.0](https://www.microsoft.com/en-gb/download/details.aspx?id=44266) |
| pypiwin32 | 219 | [219](https://sourceforge.net/projects/pywin32/files/pywin32/Build%20219/) |
| PyCrypto | 2.6.1 | [2.6.1](http://www.voidspace.org.uk/python/modules.shtml#pycrypto) |
| Ordered Dict | 1.1 | [1.1](https://pypi.python.org/pypi/ordereddict) |
| WxPython | 3.0.2.0 | [3.0.2.0](https://sourceforge.net/projects/wxpython/files/wxPython/3.0.2.0/) |
| \*UPX | 3.94w | [3.94w](https://github.com/upx/upx/releases/tag/v3.94) |

\*The [UPX Packer](https://upx.github.io/) is an optional, but highly recommended tool that the builder can use to pack the ransomware executable. UPX will allow you to reduce the size of the binary that PyInstaller produces by several Megabytes.

Once the above software is installed you will be able to launch the builder.

## How can I build Crypter?
Providing you've met the above prerequisites, building Crypter is now easy thanks to the newly added builder application.

- Run the *Builder.pyw* script in the *build* directory of this repository to launch the builder.
- Change any desired options, or leave the fields as they are to build Crypter with the default configuration.
- Click the BUILD button at the bottom of the app to start the build.
- Check the *bin* directory (created during the build) in the root of the repository for the produced binary.

## How does Crypter work?
Crypter's approach is fairly conventional, but the lack of a CnC component does result in different behaviour (see the [Crypter video demonstration](https://youtu.be/r3jaNHmkkXE)). Rather than sending the key to a remote server, Crypter instead writes it to a local file so that the files can be easily decrypted. Once executed, the following steps are taken:

1. Generates an AES-256 bit key and writes it to key.txt in the current directory
    - You can use this key in the Crypter GUI to decrypt your files
2. Searches relevant locations (network drives, user directories, etc.) for matching files
    - Locations searched depend on the configuration you specify in the Builder.
3. Encrypts all matching files
4. Displays the Crypter GUI to the victim

## Why was Crypter created?
Given Crypter's malicious capabilities, as well as the disclaimer in this README, you may be wondering why Crypter was created. The primary (and original) goal of this project was to provide a proof-of-concept which demonstrated Python's capabilities as a language for real-world malware development. 

As development continued, the focus of the project then changed to provide a tool that could be used for security training and first-hand user awareness. In this sense, Crypter could be used to perform and demonstrate a real-world ransomware outbreak within a controlled environment, the effects of which could be easily reversed.

Traditionally, compiled languages like C and C++ have been the chosen platforms of malware authors. Today however, a general advancement of platforms and tools has introduced attractive alternatives which extend these opportunities to other languages. As an incredibly popular, beginner-friendly language with an immense wealth of third party support, Python allows developers to quickly create powerful tools without the overhead of a lower-level language. These characteristics are likely responsible for the increase in Python-based malware pieces observed in recent years, and will also likely influence and impact future trends in the area. Examples of such pieces include:

+ [PWOBot](http://researchcenter.paloaltonetworks.com/2016/04/unit42-python-based-pwobot-targets-european-organizations/)
+ [PyCL](https://www.bleepingcomputer.com/news/security/pycl-ransomware-delivered-via-rig-ek-in-distribution-test/)
+ [CryPy](http://www.zdnet.com/article/python-ransomware-encrypts-files-with-unique-keys-one-at-a-time/)
+ [HolyCrypt](https://www.bleepingcomputer.com/news/security/new-python-ransomware-called-holycrypt-discovered/)

Whilst similar projects do exist on GitHub, few are structured in the same way. Crypter aims to expand upon these by providing a *cryptolocker* style Python-based ransomware piece, which can be easily customised and built.
