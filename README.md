# Cyber-Defenders-Challenge-Patrick
Write Up, Screenshots, Scripts etc. for Challenge Patrick on cyberdefender.org/blueteam-ctf-challenges

In this challenge, we were given a zipped file of a user's iPhone and were asked to answer a bunch of questions. We were given a GrayKey Extraction Report, and the /private/var folder.

For the cardinal direction the user was moving in, i exiftool -ee IMG_0002.MOV in mobile/Media/DCIM/100APPLE 

From the AXIOM pdf given i went to private/var/mobile/Library/Caches/com.apple.routined/Caches.sqlite and used DB Browser for SQLite to open it and enter the last known location.

calendar.sqlitedb in calendar table from var/mobile/Library gives the colour assigned to work

The safari browser data History.db in var/mobile/Library/History.db gives his google searches. I unfurl the google search and the ei timestamp converted to the eastern time for vermont gives the right time.

RMAdminStore-Local.sqlite gives the app with most screentime.

Then i downloaded iLEAPP to answer the rest of the questions, which i really appreciated. The GUI was really nice. I hope to create something as useful like this someday.

The rest of the questions were answered very quickly by just looking up on iLEAPP. Im not writing that down since it seems very obvious. 

![Screenshot from 2022-10-18 11-49-45](https://user-images.githubusercontent.com/24385029/203812237-aee11cb6-d941-4120-8480-8b0325b78e99.png)
![Screenshot from 2022-10-18 11-53-19](https://user-images.githubusercontent.com/24385029/203812271-9a518dd6-6085-478a-a2d2-6d05398ab442.png)
![Screenshot from 2022-10-18 11-54-02](https://user-images.githubusercontent.com/24385029/203812294-6d290a34-4863-4d8c-8efa-befc9588c903.png)
![Screenshot from 2022-10-18 11-54-53](https://user-images.githubusercontent.com/24385029/203812308-2b13cb93-1bf4-42ac-abd5-128d06f9baa5.png)
![Screenshot from 2022-10-18 12-55-33](https://user-images.githubusercontent.com/24385029/203812343-f54b79bd-d8c9-44b3-82c8-772c96550ba7.png)
![Screenshot from 2022-10-18 13-19-32](https://user-images.githubusercontent.com/24385029/203812359-6fbc9a29-1719-4394-ba43-5588acf97fdb.png)
![Screenshot from 2022-10-18 15-04-33](https://user-images.githubusercontent.com/24385029/203812374-ac21931d-875e-4e2a-a46d-ade3cefcf43f.png)

For some questions i had to use the mac deserialiser because there were nskeyed archives that i couldnt open it regularly. For eg. I needed the reddit account info, so i found the app guid from the ileapp report,but the information was an NSKeyed so I couldnt decrypt it.
![Screenshot from 2022-10-18 18-22-44](https://user-images.githubusercontent.com/24385029/203812485-46962677-dd12-48b1-b3aa-d09c8b58b420.png)

Here are the steps i followed:

1. I cloned the deserialiser.py from github.com/ydkhatri/MacForensics.git and worked the py script on the ivu21eum file with python3 deserialiser.py /home/dj/Downloads/ivu21eum
![Screenshot from 2022-10-18 23-33-04](https://user-images.githubusercontent.com/24385029/203812622-ba206f44-9bdd-4269-845b-457d86228e3c.png)

2. Then i installed plistutil using libplist-utils sudo apt-get install libplist-utils.
3. plistutil -i ivu21eum_deserialized.plist -o reddit.xml.plist
![Screenshot from 2022-10-18 23-39-40](https://user-images.githubusercontent.com/24385029/203812701-0e3b9737-11f7-4e47-a3ea-b561453934a4.png)

4. the reddit xml plist opened and i found the answers using a simple ctrl+F

In /var/installd/Library found the reboot log and using cat and grep to find when the last reboot log occurred. the installd log also shows the application that was uninstalled by its identifier
![Screenshot from 2022-10-19 00-32-58](https://user-images.githubusercontent.com/24385029/203812785-b6f3fabc-4a89-4c7e-b870-9c5f4cfbad0b.png)
![Screenshot from 2022-10-19 00-34-51](https://user-images.githubusercontent.com/24385029/203812806-dbcd078f-7d7b-4335-a0a1-4af7ce636fdc.png)


Thats it, DONE!
