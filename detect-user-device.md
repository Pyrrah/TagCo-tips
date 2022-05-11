# Detect user device

1) If you want to display a tag only for specific users (desktop, mobile, tablet, operator box to watch TV), it's possible and very easily. 
How guy? By creating an internal variable! 
First, go to Tag > Options > Variables Internes > Ajouter une variable.

2) Define the variable name with `tC.internalvars.device`, and choose "Personnalisé".

3) Put the code :
```
tC.extend({
    detectDevice : {
                get : function(){
                               var ua = (navigator ? navigator.userAgent : 'No User-Agent Provided');
                               return ua.match(/GoogleTV|SmartTV|Internet.TV|NetCast|NETTV|AppleTV|boxee|Kylo|Roku|DLNADOC|CE-HTML/i) ? 'tv'
                                               // tv-based gaming console
                                               : ua.match(/Xbox|PLAYSTATION.3|Wii/i) ? 'tv'
                                               // tablet
                                               : ua.match(/iPad/i) || ua.match(/tablet/i) && !ua.match(/RX-34/i) || ua.match(/FOLIO/i) ? 't'
                                               // android tablet                                                         
                                               : ua.match(/Linux/i) && ua.match(/Android/i) && !ua.match(/Fennec|mobi|HTC.Magic|HTCX06HT|Nexus.One|SC-02B|fone.945/i) ? 't'
                                               // Kindle or Kindle Fire
                                               : ua.match(/Kindle/i) || ua.match(/Mac.OS/i) && ua.match(/Silk/i) ? 't'
                                               // pre Android 3.0 Tablet
                                               : ua.match(/GT-P10|SC-01C|SHW-M180S|SGH-T849|SCH-I800|SHW-M180L|SPH-P100|SGH-I987|zt180|HTC(.Flyer|_Flyer)|Sprint.ATP51|ViewPad7|pandigital(sprnova|nova)|Ideos.S7|Dell.Streak.7|Advent.Vega|A101IT|A70BHT|MID7015|Next2|nook/i) || ua.match(/MB511/i) && ua.match(/RUTEM/i) ? 't'
                                               // unique Mobile User Agent
                                               : ua.match(/BOLT|Fennec|Iris|Maemo|Minimo|Mobi|mowser|NetFront|Novarra|Prism|RX-34|Skyfire|Tear|XV6875|XV6975|Google.Wireless.Transcoder/i) ? 'm'
                                               // odd Opera User Agent - http://goo.gl/nK90K
                                               : ua.match(/Opera/i) && ua.match(/Windows.NT.5/i) && ua.match(/HTC|Xda|Mini|Vario|SAMSUNG-GT-i8000|SAMSUNG-SGH-i9/i) ? 'm'
                                               // Windows Desktop
                                               : ua.match(/Windows.(NT|XP|ME|9)/) && !ua.match(/Phone/i) || ua.match(/Win(9|.9|NT)/i) ? 'd'
                                               // Mac Desktop
                                               : ua.match(/Macintosh|PowerPC/i) && !ua.match(/Silk/i) ? 'd'
                                               // Linux Desktop
                                               : ua.match(/Linux/i) && ua.match(/X11/i) ? 'd'
                                               // Solaris, SunOS, BSD Desktop
                                               : ua.match(/Solaris|SunOS|BSD/i) ? 'd'
                                               // Desktop BOT/Crawler/Spider
                                               : ua.match(/Bot|Crawler|Spider|Yahoo|ia_archiver|Covario-IDS|findlinks|DataparkSearch|larbin|Mediapartners-Google|NG-Search|Snappy|Teoma|Jeeves|TinEye/i) && !ua.match(/Mobile/i) ? 'd'
                                               // assume it is a Mobile Device (mobile-first)
                                               : 'm';
                }
    }
});
```
4) Don't forget to choose the step "Declared in container".
Be carefull, by default all containers are selected.

5) Defined the description :
*It detects the user device and give the output "d" for desktop, "m" for mobile, "t" for tablet and "tv" for television or boxes*

6) That's all Folks!
Now, we can use your internal var `tC.internalvars.device with a constraint :
"d" for desktop	:desktop_computer:, "m" for mobile :iphone:, "t" for tablet :grey_question: and "tv" for television or boxes :tv: