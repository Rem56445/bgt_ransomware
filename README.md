# bgt_ransomware
a ransomware made in the bgt (blastbay game toolkit) programming language
# disclamer

This program has been developed for educational purposes only, in order to explain the basic principles of a simple ransomware as well as for detailing how social engineering can be used in order to facilitate infection. The author or publisher of this program shouldn't be held responsible for any damage arising, directly or indirectly, from running this program or interacting with it in any way, including copying, examining the source, incorporating it in other programs, etc.

# motivation

In the blind community, there was an ecosystem called bgt(blastbay game toolkit). Within this package, the users would have access to several utilities to allow the faster making of audiogames. Among those we can find things like very primitive networking, audio with only ogg and wav sound playback, no 3d or hrtf support, tts but only with the microsoft speech API version 5 which is now being replaced by one core, etc.  
The engine became obsolete a long time ago, yet there are people continuing to use it. Though not big issues at the time, here are some limitations of the ecosystem:

* very rudimentary C calling support, specifically no callbacks and no structs. That greatly limits the extensibility of the engine, making the ecosystem more walled in.
* the executables made with it are almost all the time flagged by antiviruses, so it has become an accepted thing that people open wholes in their protection for the bgt games. This is not a good practice for anything, not only bgt, but since we're here to destroy trust in this tool which shouldn't exist anymore in the first place, I am making use of that to circumvent protection.
* 32 bit only support. The 32 bit architecture is being fazed out, so bgt executables might not run in future versions of windows.
* networking can't be done unless the server is also written in bgt, which means the server has to run windows.
* and many more!

Therefore, I decided to show people that bgt shouldn't be used or trusted anymore, by making this malware that makes use of the fact security wholes are being open for it on the computers of everyone who play bgt games.

# behaviour

Here I will explain mostly the function of the malware, without details about esthetic features, such as music or non-important speech messages. The code is here, so explore it at your leasure

This program pretends it is an antivirus, cleanning viruses and stuff from your computer. To add insult to injury, it uses obvious words to give it away, such as free and with no viruses, etc.

* First, it introduces itself to you, telling you what functions it has.
* Afterwards, it picks a random location to begin the infection from. Possibilities include documents, desktop, program files and system32. It will speak a message for each location
* Next, it builds an in-memory list of absolute paths to files from the directory it chose in the previous step, as well as files in any subfolder by recursively walking the filesystem. In order not to cause a stack overflow runtime error, the algorithm used doesn't imploy true recursion, rather it simulates one by using a stack of paths.  
While doing this, it will speak a message like indexing files...
* continuing on, for each file in the path list obtained in the previous step, it uses aes256 with a 128 character key composed of randomly chosen characters. The encrypted file is named like the original one, but it has the extension of .ransomware.encrypted. The original will, of course, be deleted. Also, the key will be copyed to your clipboard, for all the good it'll do at that point.
* finally, it will tell you never to use bgt again, don't develop with it and don't open security wholes in your computer by making exclusions for programs written in such an outdated, insecure and limited engine. The text your speech engine will speak is much longer than that, but here I summarised it as best I could.

# notes

The aes encryption algorithm bgt uses won't be decrypted by using an aes library written in python or another language, since several parameters are supplyed by the engine and not known to the public.  
The task of writing a decryptor in bgt or discovering the parameters supplyed to aes by the engine is not disclosed here, as to make of it an interesting and possibly fun activity. Hint: with the provided code, it's much easier to make a decryptor in bgt, since the key is on the clipboard and most of the required code is available here.  
In stead of using a graphical user interface, it uses an invisible one and the tts capabilities of bgt in order to convey information.  
No particular care has been taken to write or butify the code in any way, so it may be all over the place. This is another part of the challenge, you have to figure out the details of how the malware works, beyond the explained things.

    
