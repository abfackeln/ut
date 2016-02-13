## ASU Frequently Asked Questions

Q. What happened to the abfackeln ut-linux installer?

A. After close to three years of helping people install Unreal Tournament on their Linux boxes to enjoy a superior gaming system, my installer is no longer supported.  If you read the FAQ and the Install information on this page then you will realize that it is no longer necessary.  If you really need to get a copy of it or if you are a collector of ancient software, you can check out the deprecated site here.

Q. Is ASU available for Microsoft servers?

A. No.

### Starting the Server

Q. Okay, I have installed the dedicated server and I have installed ASU.  Now what?  How do I start the server?

A. I am going to assume that you have figured out how to start ASU.  After you start ASU, you will find an option called "Install Init Script."  Select this, answer all of the questions, and it will tell you what to do.  
Notice: If you are using ASU 0.5, you should install the asu-init-installer patch before doing this.

Q. I can not start my server.  Every time I try, it says this (below), what is happening? 
Starting Unreal Tournament : Process is already running. Not Started

A. If this happens, try using "ucc.init restart".

Q. I can not start my server.  Every time I try, it says this (below), what is happening? 
./ucc-bin: error in loading shared libraries: libSDL-1.2.so.0: cannot open shared object file: No such file or directory

A. I am not sure why this happens but, thanks to UR1_CAMPER_KILLER, I think we have a solution.  Just go to your System directory and type:
ln -s libSDL-1.1.so.0 libSDL-1.2.so.0

Q. I can not start my server.  Every time I try, it says this (below), what is happening? 
error while loading shared libraries: cannot open shared object file: cannot load shared object file: No such file or directory

A. This happens when a required shared object (.so) file is missing .. (most often the files which are missing are libX11.so.6 and libXext.so.6) .. to know for certain, try going in to the System directory (located in the unreal game directory) and entering the following command: 
ldd *.so | grep not.found 
If this command returns anything then you are missing some required library files.  For RedHat users, you can get the X11 and Xext libraries from the RPM by the name of XFree86-libs.

### Common Problems

Q. My server crashes whenever it gets to a specific map.  The error message says something about finding an "Editor" package.  What is going on?

A. You need to get Editor.u into your System directory.  For some reason this is not included in the dedicated server package but it is in the full linux install.  You can also copy this file from a windows machine if it is the same UT version because the .u files are platform independent.

Q. All of the players look like they are sliding; they are not animated properly -- do you know what is wrong?

A. This is most likely because you have installed compressed or "enhanced" textures from a bonus CD.  Stop doing that.  Reinstall or copy the original texture files from your CD over top of the ones in your Textures directory.

Q. Some people are having trouble connecting to the UT server.  Even though it is running, they are getting connection refused messages.  Why does this happen?

A. This is most likely because the Download Redirection is broken.  Try disabling it and see if you still have the same problem.

### Running the Server

Q. If i am running a UT server behind a firewall, which ports do i need to open?

A. Firstly, the UT server needs to be able to listen to the TCP port which you have selected (if any) for your web admin port.  It will also need to listen to several UDP ports and they are not always the same because they depend on which port you have selected for your game port.  If you have selected 7777 as your game port (this is the default) then your server will want to listen to UDP ports 7777, 7778, 7779, 7780, and 7781.  And, finally, UDP port 9999 is required for outgoing UDP traffic to the ngWorldStats site and UDP port 27900 is required for outgoing UDP traffic to the master server. 

### Server Administration

Q. Why can I not view my web admin page?

A. For some reason, Linux 2.4 kernels are incompatible with the HTTP code that UT uses to display the web admin pages.  This has reportedly been fixed in Linux 2.4.18.  Additionally, there have been attempts to fix this by setting up a hack proxy using the netcat utility.  there is discussion on how to do this on The Admin Page forums.  Click Here

Q. Why is it that I can't get the Web Admin to actually write to the UnrealTournamemnt.ini file?  I make my changes, I apply my changes and the ini file is left unchanged.  Does this Remote Web Admin tool work at all ?

A. The UnrealTournament.ini file is not rewritten in real time.  The way that it works is the file is read only once when you start the server and it is updated only when the map changes.  Therefore, any change that you make will not take effect until the map changes.  This is also why you can not edit the ini file while the server is running.  This also means that you can not use ASU to edit the settings while the server is running.

Q. "The server runs great but lags out with very high pings just as a new map starts."

A. Try the Optimization Menu in ASU.

Q. The ping rate to my UT server is about five times more than it is when I ping the server from the console.  Why is my ping so bad?

A. Ya.  I know.  Okay, look.  The "ping" in UT is not a standard "ping" -- it takes into account the server load and so on because the "ping" is handled by the server itself and not a dedicated "ping" responder like it should be.  I have no idea why they did this because it just confuses people.

### Advanced Server Administration

Q. Is the file DM-Mapname.unr.uz the same as the file DM-Mapname.unr (without the ".uz")?

A. NO!  The .uz file is compressed and must be decompressed before it will work.

Q. How do you compress or decompress map files?

A. For some reason this is very temperamental and, as far as I can tell, you must supply a complete path name to your map file.  Furthermore, the decompress always wants to decompress to the System directory. Anyway, the following commands should work, executed from the game directory.
Compression:
./ucc compress /usr/games/ut-server/Maps/DM-Barricade.unr -nohomedir
Decompression:
./ucc decompress /usr/games/ut-server/Maps/DM-Barricade.unr.uz -nohomedir
mv System/DM-Barricade.unr Maps

Q. When I try to run the server, using FreeBSD, I get this message: 
ELF binary type "3" not known. 
Abort 
How do I make it work?

A. You need to have Linux support enabled.

Q. I installed Tactical Ops 3.4 and it says that it can not find TOST.  Am I doing something wrong?

A. No, the people who package Tactical Ops refuse to make the Linux version work out-of-the-box.  I have no idea why.  Anyway, go into the .ini file and find the line where it sets 
Paths=../tost/system/410/*.u 
and type it properly, like so: 
Paths=../Tost/System/410/*.u 

Q. How do I make Tactical Ops 2.0 work ?

A. The umod for Tactical Ops 2.0 is incompatible with the linux umodpack script so you are going to have to do a manual install.  After doing a manual install you can still make an .init script with ASU but you will have to choose game type "SW" and then modify the .init script afterward to edit the map name, i.e.:
MYMAP=TO-RapidWaters2

### Problems with ASU 0.4

Q. I am getting the following error when I try to use the ASU patch command: 
.../legacy-asu-script-0.1.sh: line 11: syntax error: unexpected end of file

A. This only happens on some systems and it will be fixed in ASU 0.5, thanks to Chad Beattie who was able to track down the problem.  I have also prepared a patch to fix the patcher (believe it or not) in ASU 0.4, available here: asu-0.4-patchfix-0.1-patch.tar.gz

---
ASU is currently in its beta-testing phase, and is being offered free without warrantee (as always).  If you have any problems, comments or suggestions please visit the abfackeln.com Unreal Tournament for Linux support page at http://ut.abfackeln.com/support.html
