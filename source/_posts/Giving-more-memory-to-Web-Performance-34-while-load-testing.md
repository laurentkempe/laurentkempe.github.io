title: Giving more memory to Web Performance 3.4 while load testing
date: 9/8/2008 10:33:28 PM
updated: 5/7/2010 7:45:41 AM
tags: ["Note to self"]
---
First do not trust their documentation! The launch anywhere (lax) file change doesn’t make it.

Do it by your own, with such a command:

"C:\Program Files\Web Performance Suite 3.4\webperformance.exe" -vm "C:\Program Files\Web Performance Suite 3.4\jre\bin\javaw.exe" -vmargs **-Xmx512M -Xms512M **-jar "C:\Program Files\Web Performance Suite 3.4\startup.jar" -os win32 -ws win32 -arch x86

Thanks Robert for the support.
