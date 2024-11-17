# **Dummy Drucker / Nirwana Drucker / NUL oder NULL Drucker anlegen / einrichten**

Für eine Terminalserver-Umgebung brauchte ich einen anderen Standarddrucker - da die Benutzer Ihren Standarddrucker frei wählen können, das beim ersten Start aber natürlich nicht getan haben, hat Windows Ihnen einen ausgesucht.
Windows geht das ganz unproblematisch an: es wurde einfach der vorne im Alphabet genommen.
Leider war das hier die Druckstrasse ...
Als Lösung habe ich einen Dummy-Drucker als den ersten verfügbaren eingerichtet - dieser Drucker druckt ins nichts / Nirwana. Alle Ausdrucke auf diesem "Drucker" werden einfach verworfen.
Wer so etwas mal braucht - so geht es:
Wir gehen zu den Druckern und legen einen neuen an:
![Dummy-Drucker-001.png](unnamed_a013ac6ededa4e169b3dbd5ce9a1fa6f.png)![group](group.png)
Es muss ein lokaler Drucker sein (den wir gerne später als Netzwerkdrucker freigeben können)
Wir erstellen einen neuen, lokalen Anschluss:
![Dummy-Drucker-002.png](unnamed_5fb8d16c2720497db2ebd6899be578c7.png)![group](group.png)
Den wir `**NUL:`** nennen!
![Dummy-Drucker-003.png](unnamed_287d06ca6f4c469a8b22d3081c8eaee9.png)![group](group.png)
`**NUL:`** kommt von NULL = 0 = ins "Nichts" bitte!
Dann müssen wir noch einen Druckertreiber wählen - nehmt bitte unbedingt einen von den in Windows eingebauten, Der `**HP Laserjet `** z.B.
![Dummy-Drucker-004.png](unnamed_c039871089764334a2817efdae849217.png)![group](group.png)
Den Namen lassen ich mit "A" anfangen damit der Drucker ganz vorne steht und ggf. von Windows automatisch genommen wird:
![Dummy-Drucker-005.png](unnamed_f8cda88b436d46e2b83cfe0be037e5ed.png)![group](group.png)
Den Drucker können wir auch freigeben - da wir den Windows-Treiber genommen haben sollte sich jeder damit verbinden können.
![Dummy-Drucker-006.png](unnamed_b8db0672f42d47cc80d4af5974273ca3.png)![group](group.png)
![Dummy-Drucker-007.png](unnamed_5715bd6fa416429384c2e2e3444ea7c8.png)![group](group.png)
Falls der Drucker im Active-Directory angezeigt werden soll müsst Ihr nachträglich noch den entsprechenden haken setzten:
![Dummy-Drucker-008.png](unnamed_f4188f3f8a144e62a95b4715c333e861.png)![group](group.png)
--[Bernhard Linz](http://znil.net/index.php?title=Benutzer:BLinz) 11:18, 27. Nov. 2012 (CET)

---

**
		Kommentare
**
**
Jojo 148 Tage  zuvor
Punkte 0![thumbs-up.gif](unnamed_81f76d1c2dbc4134830ff46e8026695f.gif)[nofollow](http://znil.net/index.php?title=Spezial:Anmelden&returnto=Dummy_Drucker_%2F_Nirwana_Drucker_%2F_NUL_oder_NULL_Drucker_anlegen_%2F_einrichten)![thumbs-down.gif](unnamed_81f631d4a39241a79777a4774c66e0a8.gif)[nofollow](http://znil.net/index.php?title=Spezial:Anmelden&returnto=Dummy_Drucker_%2F_Nirwana_Drucker_%2F_NUL_oder_NULL_Drucker_anlegen_%2F_einrichten)
**
Super Anleitung. Brauchte einen Dummy Drucker für Auftragsbestätigungen die die Branchensoftware zum buchen benötigt, aber ich nicht als Papierausdruck. Hatte es sonst mit einem Druck in eine Datei gelöst, die immer überschrieben wurde.
Funktioniert einwandfrei und vor allem auf Anhieb. DANKE!
[nofollowPermalink](http://znil.net/index.php?title=Dummy_Drucker_/_Nirwana_Drucker_/_NUL_oder_NULL_Drucker_anlegen_/_einrichten#comment-286)  | [nofollowAntworten](http://znil.net/index.php?title=Dummy_Drucker_/_Nirwana_Drucker_/_NUL_oder_NULL_Drucker_anlegen_/_einrichten#end) 
**
[nofollowBLinz](http://znil.net/index.php?title=Benutzer:BLinz) 147 Tage  zuvor
Punkte 0![thumbs-up.gif](unnamed_81f76d1c2dbc4134830ff46e8026695f.gif)[nofollow](http://znil.net/index.php?title=Spezial:Anmelden&returnto=Dummy_Drucker_%2F_Nirwana_Drucker_%2F_NUL_oder_NULL_Drucker_anlegen_%2F_einrichten)![thumbs-down.gif](unnamed_81f631d4a39241a79777a4774c66e0a8.gif)[nofollow](http://znil.net/index.php?title=Spezial:Anmelden&returnto=Dummy_Drucker_%2F_Nirwana_Drucker_%2F_NUL_oder_NULL_Drucker_anlegen_%2F_einrichten)
**
Immer gerne :-)
[nofollowPermalink](http://znil.net/index.php?title=Dummy_Drucker_/_Nirwana_Drucker_/_NUL_oder_NULL_Drucker_anlegen_/_einrichten#comment-287) 
nofollow
**Kommentar hinzufügen:**
Gebe hier einen Kommentar ein. Du kannst einen beliebigen Namen oder eine Email-Adresse als Namen angeben.
Wenn du dich [einloggst](http://znil.net/index.php?title=Spezial:Anmelden) wird automatisch dein Benutzername genommen.
Links bitte mit '''http://''' beginnen lassen.
Name oder Emailadresse:
Kommentar:
[Kategorien](http://znil.net/index.php?title=Spezial:Kategorien): 

- [Windows](http://znil.net/index.php?title=Kategorie:Windows&action=edit&redlink=1)- [Windows 7](http://znil.net/index.php?title=Kategorie:Windows_7&action=edit&redlink=1)- [Windows Server 2000](http://znil.net/index.php?title=Kategorie:Windows_Server_2000&action=edit&redlink=1)- [Windows Server 2003](http://znil.net/index.php?title=Kategorie:Windows_Server_2003&action=edit&redlink=1)- [Windows Server 2008](http://znil.net/index.php?title=Kategorie:Windows_Server_2008&action=edit&redlink=1)- [Windows Vista](http://znil.net/index.php?title=Kategorie:Windows_Vista&action=edit&redlink=1)- [Windows XP](http://znil.net/index.php?title=Kategorie:Windows_XP&action=edit&redlink=1)

