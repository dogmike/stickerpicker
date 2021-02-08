# Maunium sticker picker
A fast and simple Matrix sticker picker widget. Tested on Element Web, Android & iOS.

## Instructions
This only seems to work on Linux systems with Python3. I managed to get it working on Windows in WSL (Ubuntu). 

### Setup ###
1. If you're on Windows, go to the Windows store and install the Windows Subsystem for Linux. Or however they do it these days.
2. On Linux, make sure you upgrade your package manager, and have python3 installed. You'll need to install python3 and python3-pip if you haven't already. Install git, too. Oh, and make an account on https://github.com.
3. Go to https://github.com/maunium/stickerpicker and fork it. On your computer, clone stickerpicker from your own repo (`git clone`). `cd` into the repository folder and run `pip3 install .` to stage it.
4. Then go to your GitHub.com repository's settings and (scroll down to GitHub Pages) put the Master branch on GitHub Pages for basic hosting. It'll make a URL at github.io that'll you'll use in Element for your own sticker picker.

### Using `sticker-pack`
Create a folder for your raw sticker packs: `mkdir raw` Then download some stickerpack zips from THE ARCHIVE (ask Nari!), and unzip each into the raw directory. Copy the name of each sticker zip onto the folder, since each had a random name. Remove the `_pack_png` from the end of their name (the program will use the folder name as the name of the pack, so you want it to look nice). Once you have them all, make sure you're back into the main repository directory (the one with README.md). Call `sticker-pack --add-to-index web/packs raw/sticker_pack_folder_name_here` for each pack. (You can can type raw/ and then the first few letters of the pack name, then press the Tab button to auto-complete.) The first time through, it'll ask for the server address and then the auth code, which you'll find on Element in your user settings (click your user icon) at the very bottom of Help & About. It'll take a moment to upload each file and edit the index. Then you `git add web`, `git commit` (press Ctrl+X then Y then Enter if an editor pops up) and `git push`. (You might need to set your Git username and stuff, first, but instructions will appear onscreen.) 

If you want to skip all that and use my stickers, that's better than nothing, so you can skip those steps.

### Adding the new sticker picker to Element
Go to Element.
First, if clicking the sticker button in the chat bar makes you search for stickers, and that just brings up a big empty box, you'll need to find the cookie icon in your URL bar and click through to an option about allowing third-party cookies. (I guess the integration manager needs a cookie.) 
Visit the Room Info from the top right, click Room Settings, go to Advanced, then open DevTools and use "Send Account Data". Send an event called `m.widgets` with the following code: (Replace my GitHub Pages username with your own, if you've made a sticker picker.)

```json
{
  "stickerpicker":{
    "content":{
      "type":"m.stickerpicker",
      "url":"https://dogmike.github.io/stickerpicker/web/?theme=$theme",
      "name":"Stickerpicker",
      "data":{}
    },
    "sender":"@you:picker.url",
    "state_key":"stickerpicker",
    "type":"m.widget",
    "id":"stickerpicker"
  }
}
```

That should work! You'll probably need to restart Element.

## Resources
There's a [wiki](https://github.com/maunium/stickerpicker/wiki):

* [Creating packs](https://github.com/maunium/stickerpicker/wiki/Creating-packs)
* [Enabling the widget](https://github.com/maunium/stickerpicker/wiki/Enabling-the-widget)
* [Hosting on GitHub pages](https://github.com/maunium/stickerpicker/wiki/Hosting-on-GitHub-pages)

If you prefer video tutorials, [Brodie Robertson](https://www.youtube.com/c/BrodieRobertson) has made a great video on setting up the picker and creating some packs: https://youtu.be/Yz3H6KJTEI0.

## Preview
### Element Web
![Element Web](preview-element-web.png)

### Element Android
![Element Android](preview-element-android.png)

### Element iOS (dark theme)
![Element iOS](preview-element-ios.png)
