# Setting up a Mac

> ### Optional: Reinstall macOS
> Reinstall macOS using this guide: https://support.apple.com/en-gb/guide/mac-help/mchlp1599/mac

This includes a lot of free apps I use on my Mac. I have a comprehensive list of these in [Github](https://github.com/jamesjingyi/free-mac-apps) and [Google Sheets](https://docs.google.com/spreadsheets/d/1QwpL1hjc878nSpuWTZwgIOyCc4r4pMusmxD6eC2UIXA/edit?usp=sharing).

## Preparation
I have two files included in this repo.

 1. `packages.txt` - These are all the packages I want installed from Homebrew
 2. `mas-apps.txt` - These are all the packages I want installed from the Mac App Store

For the commands later I have downloaded these to the `Downloads` folder (`Users/<username>/Downloads`) 

Open the Terminal, `cd` to the `Downloads` folder using:
```
cd Downloads/
```

## 1 - Install apps
### 1.1 - Homebrew
**1.1.1** - Install Homebrew using the following command:
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
**1.1.2** - Then install all the packages recursively in `packages.txt` by running the command:
```
brew install $(grep -v '^--cask' packages.txt) && brew install --cask $(grep '^--cask' packages.txt | sed 's/^--cask //')
```
`brew install` can install multiple packages at once by just queueing them up, one after another (e.g. `brew install gh bitwarden-cli`), however has to install `cask` and `non-cask` packages separately. The above command separates this into two commands.
### 1.2 - Mac App Store
**1.2.1** - Using the `mas` package installed in **Step 1.1.2**, install previously purchased/installed apps recursively using the following command:
```
grep -v '^\s*#' mas-apps.txt | awk '{print $1}' | xargs -n 1 mas install
```
**1.2.2** - iOS/iPadOS Apps cannot be downloaded using `mas`. You have to download these manually. Currently the two I have installed are:
|App name|Link|
|--|--|
|`BlueSky`|Mac App Store - [BlueSky](https://apps.apple.com/gb/app/bluesky-social/id6444370199)|
|`X`|Mac App Store - [BlueSky](https://apps.apple.com/gb/app/x/id333903271)|
### 1.3 - Other sources
**1.3.1** - The other apps I install outside of these two places are:
|App name|Link|
|--|--|
|`Lossless Switcher`|Github - [Lossless Switcher](https://github.com/vincentneo/LosslessSwitcher)|
|`OpenType Feature Freezer`|Github - [OpenType Feature Freezer](https://twardoch.github.io/fonttools-opentype-feature-freezer/)|
|`ShazamScrobbler`|Github - [ShazamScrobbler for Mac](https://github.com/ShazamScrobbler/macos-app)|
|`AirBattery`|Github - [AirBattery](https://lihaoyun6.github.io/airbattery/)|
|`TheBoringNotch`|Github - [TheBoringNotch](https://github.com/TheBoredTeam/boring.notch)|
**1.3.2** - `TheBoringNotch` is not yet signed by Apple, so when first launched, it will show a popup saying it is untrusted. Click `Okay`, then on your Mac go to `Settings` > `Privacy & Security`  and scroll until you see a button saying `Open Anyway`.
### 1.4 - Additional app downloads
**1.4.1** - **Adobe**:  `brew` will have installed `Creative Cloud` but it will not have installed the apps. Sign in and download the apps.
**1.4.2** - **Xcode**: Xcode needs to install additional bits. Launch it and download the relevant environments.

## 2 - Install fonts
### 2.1 - Google Fonts
Install all the fonts from the [`google/fonts`](https://github.com/google/fonts) repository by doing the following:
```
cd ~/Library/Fonts/
```
```
git clone https://github.com/google/fonts.git google-fonts
```

> **Updating fonts** 
> ``` cd ~/Library/Fonts/google-fonts/ ``` 
> ``` git pull ```
> 
> **Removing fonts** 
> ``` rm -rf ~/Library/Fonts/google-fonts/ ``` 
> Source: [How to Install ALL Google Fonts on
> macOS](https://www.junian.net/tech/macos-google-fonts/)

### 2.2 - Apple Fonts
I usually need to use some of Apple’s fonts (like San Francisco), so I download them from Apple [here](https://developer.apple.com/fonts/).

### 2.3 - Fontshare
There is no way to install all of these at once. Unfortunately you have to go and select 'Download' on each [here](https://www.fontshare.com).

## 3 - Settings
### 3.1 - System Preferences
#### 3.1.1 - Desktop and Dock
I turn on `Automatically hide and show the Dock` and set the size and magnification as shown here:
![Screenshot of the Dock settings in macOS](Desktop-and-Dock-settings.png)

#### 3.1.2 - Windows
I turn on `Hold ⌥ key while dragging windows to tile` and turn off `Tiled windows have margins`

### 3.1.3 - Mission Control
I turn on `Group windows by application`
![Screenshot of the Windows and Mission Control settings in macOS](Windows-and-Mission-Control-settings.png)

### 3.1.4 - Trackpad
I turn on the gesture for `App Exposé` - `Swipe Down with Three Fingers`

### 3.1.5 - Keyboard Shortcuts
Since I use `Shottr` for screenshots, I change the `Copy` default to add an `⌥` modifier e.g. `⇧` + `⌘` + `3` -> `⌥` + `⇧` + `⌘` + `3`
Also since I use `Raycast` instead of `Spotlight`, I change from `⌘` + `Space` to `⌥` + `Space`
![Screenshot of the Screenshot keyboard shortcuts in macOS](Screenshot-shortcuts.png)
![Screenshot of the Spotlight keyboard shortcuts in macOS](Spotlight-shortcuts.png)

### 3.2 - Preinstalled Apps
#### 3.2.1 - Finder
##### 3.2.1.1 - Preferences
Finder’s sidebar is never used enough imo, so I open Finder, do `⌘` + `,` to open `Preferences` and:
- In `General`, ensure `Sync Desktop & Documents folders` is checked since I want my Desktop and Documents to be synced via iCloud
- In `Sidebar` select everything (apart from `On My Mac`)
##### 3.2.1.2 - Other customisations
- I drag `Documents` and `Desktop` from the `iCloud` section in the Sidebar up to the `Favourites` section above (this just makes much more sense for me)
- I turn on the `Path Bar` by going to `View` > `Show Path Bar`
- In my `Downloads` folder I set this up for how it best works for me:
	- I always want it to be sorted by `Date Last Added`, so I set this for both `View` > `As Icons` and `View` > `As List`
    - In `List` view I also add `Date Modified` as this can sometimes be useful
##### 3.2.1.3 - In other apps
When you’re in other apps, the selection interface can be hard to use, especially with your `Downloads` folder which can often be shown in the `Columns` view. In this view, it sorts alphabetically and you can’t seem to find blank space to right click and sort by `Date Last Added`. To rectify this, change it to `Icons`, and you’ll be able to find space in-between documents to right click.

### 3.2.2 - Safari
I am not sure why, but Safari likes to default to open with a new window every time you start it up. I always change it to:
`Safari opens with:` `All windows from last session`

### 3.2.3 - Dock
We already talked about the Dock settings before, but I like to separate out the items on my Dock using spacers. There are two types of spacer, small and regular. Regular is the same size as a full app, whereas small is half the width. I use small spacers. 

To add these, you have to run the corresponding command in `Terminal`. Sometimes this doesn’t work, so re-run it until it adds one. Once one is added, drag and position it before adding another — the success rate of adding another seems to go up if you drag the one you just added away.

The commands to add spacers are as follows:

#### 3.2.3.1 - Small spacer
```
defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="small-spacer-tile";}'; killall Dock
```

#### 3.2.3.2 - Large spacer
```
defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="spacer-tile";}'; killall Dock
```
## 3.3 - Replacing default macOS functions
### 3.3.1 - Raycast
I prefer Raycast to Spotlight — it has many more functions and I can customise it more. I am by no means a power user, but I have adjusted it so that it works for me.
#### 3.3.1.1 - Extensions
Raycast has a Store which allows you to install `Extensions` which can run functions on your Mac, both system and app-specific. When I first started using Raycast, I ended up adding loads and loads of extensions, and both forgetting about functions, and also being overwhelmed when I searched for a function. There a few ways I have combatted this:
1. **I only install Extensions I will actually use** — This seems simple, but I am definitely an optimistic downloader. I have tamed this somewhat. If I am browsing the Store, I carefully check my own workflow to identify if I think an extension would actually make sense (do I use this function commonly? Would I actually think to use Raycast rather than a web app?).
2. **I only enable the parts of the Extensions that I want** - This is something I didn’t really think about properly until recently, but this actually made my menus much less overwhelming. In the `Extensions` tab, I go through and expand each Extension and uncheck all the Commands which duplicate other functionality, or I just don’t want.
3. **I add Aliases** - See the below section, I think these are great!

Below I have written out the Extensions I have installed, and the Commands I have enabled for each of them, often slimmed down significantly (if you search for them in the Store, lots have a lot more than the number I have enabled!). Any spaces have been shown as underscores (`_`).

| Extension Name | Commands Enabled | Command Alias |
|:----|:---:|:---:|
| Apple Maps Search | Search Maps | - |
| Arc | Open New Little Arc Window<br>Search Tabs | `little_arc`<br>`arc_search` |
| Bitwarden Vault | Generate Password<br>Search Vault | `-`<br>`bw` |
| Brew | Clean Up<br>Search<br>Show Installed<br>Show Outdated<br>Upgrade | `-`<br>`-`<br>`-`<br>`-`<br>`brew_upgrade` |
| Calendar | My Schedule | `sch` |
| Change Case | - | `case` |
| Clipboard History | - | `clip` |
| Coffee | Caffeinate<br>Caffeinate For<br>Caffeinate While<br>Decaffeinate | `caf`<br>`caf_for`<br>`caf_while`<br>`decaf` |
| Color Picker | Color Names<br>Convert Color<br>Pick Color | `colour_ _name`<br>`colour_conv`<br>`colour_picker` |
| Define Word | - | `def` |
| Google Search | - | `google` |
| Kill Process | - | - |
| Link Cleaner | - | `link_clean` |
| Music | Add to Library<br>Next Track<br>Pause<br>Play<br>Previous Track<br> | `-`<br>`next`<br>`pause`<br>`play`<br>`back` |
| Navigation | Search Menu Items<br>Switch Windows | - |
| Notion | Search Notion | `notion_search` |
| Quicklinks | Export Quicklinks<br>Import Quicklinks | - |
| Raycast | Confetti<br>Manage Fallback Commands<br>Quit Raycast<br>Refresh Apps and Settings<br>Reset Raycast Window Position<br>Run Last Command<br>Search Quicklinks<br>Store<br>Walkthrough | -<br>-<br>-<br>-<br>-<br>-<br>-<br>`extensions`<br>- |
| Raycast Settings | Al<br>About<br>Account<br>Advanced<br>Cloud Sync<br>Extensions<br>General<br>Organizations | - |
| Ruler | - | - |
| Screenshot | All in One<br>Capture Area<br>Capture Screen<br>Capture<br>Timer<br>Capture Window<br>Capture Window To Clipboard<br>Capture and Annotate<br>Capture to Clipboard | -<br>-<br>`cap_s`<br>`cap_w`<br>-<br>-<br>- |
| Screenshots | Paste Recent Screenshot<br>Search Screenshots | - |
| Search Browser Tabs | - | `browser` |
| Search Device | - | - |
| Search Emoji & Symbols | - | `emoji` |
| Search Files | - | - |
| Shortcuts | - | - |
| Snippets | Create Snippet<br>Export Snippets<br>Import Snippets<br>Search Snippets | - |
| System | Empty Trash<br>Lock Screen<br>Quit All Applications<br>Set Volume to 0%<br>Shut Down | -<br>-<br>-<br>`vol_0`<br>- |
| Translate | - | - |
| View 2FA Codes | - | `2fa` |
| Webpage to Markdown | - | `webpage_ _markdown` |
| Wifi Password Reveal | - | `wifi_reveal` |
| Window Management | Bottom Half<br>Bottom Left Quarter<br>Bottom Right Quarter<br>Left Half<br>Maximize<br>Top Left Quarter<br>Top Right Quarter | `win_b`<br>`win_bl`<br>`win_br`<br>`win_l`<br>`win_fs`<br>`win_t`<br>`win_tl`<br>`win_tr` |

#### 3.3.1.2 Aliases
Adding Aliases actually was actually a game-changer. These allow you to assign characters to Extension (which includes each app), meaning when you type these, Raycast suggests this first. This even works if you haven’t typed the whole of the Alias, suggesting it above the default search.I now have double or triple letter Aliases set so I can quickly launch them.

These are also good for when something has been renamed, or if you can’t remember the name of something but can remember its function (or want to group applications by function). For example I have **Terminal** set to `term` and **Warp** set to `term2`, and **X** set to `twi`.

I have the Extensions Aliases above, but for apps specifically I have:
| App Name | Alias |
|:----|:---:|
| Adobe Acrobat | `acrobat` |
| Adobe Illustrator | `il` | 
| Adobe InDesign | `id` |
| Adobe Lightroom | `lr` |
| Adobe Media Encoder | `media_enc` |
| Adobe Photoshop | `ps` |
| Adobe Premiere Pro | `premiere` |
| App Store | `app` |
| App Cleaner | `clean` |
| Arc | `arc` |
| Blender | `blend` |
| Bluesky | `bs` |
| Calendar | `cal` |
| ChatGPT | `ch` |
| Figma | `fig` |
| Final Cut Pro | `fcp` |
| Firefox | `ff` |
| ImageOptim | `img` |
| Keynote | `key` |
| Logic Pro | `lp` |
| Messages | `msg` |
| Messenger | `fb_messenger` |
| Microsoft Excel | `excel` |
| Microsoft PowerPoint | `powerpoint` |
| Microsoft Teams | `teams` |
| Microsoft Word | `word` |
| Music | `music` |
| News | `news` |
| Notes | `notes` |
| Notion | `notion` |
| Numbers | `numbers` |
| Pages | `pages` |
| Perplexity | `pp` |
| Photos | `photos` |
| Podcasts | `podcasts` |
| QuickTime Player | `qt` |
| Safari | `saf` |
| Simulator | `sim` |
| Sketch | `sk` |
| Sketch Beta | `skb` |
| Slack | `sla` |
| System Settings | `pref` |
| Terminal | `term` |
| TextEdit | `te` |
| Visual Studio Code | `vsc` |
| Warp | `term2` |
| WhatsApp | `wa` |
| X | `twi` |
| Zen Browser | `zen` |


### 3.2.2 - Ice
To tidy up my menu bar I use `Ice`, where I place things is as follows:
![Screenshot of my Ice menu bar arrangement](Ice-settings.png)

### 3.2.3 - Shottr
I use `Shottr` instead of macOS’s built in screenshot utility. I prefer that it allows you to mark up, edit, crop, measure, and more!

It also has a super useful OCR feature which allows you to select an area on the screen and extract the text from it. 

Since I want it to replace the default screenshots in macOS, I set it up to:
| Command | Shortcut 
|:----|:---:|
| Fullscreen screenshot | `⇧` + `⌘` + `3` | 
| Area screenshot | `⇧` + `⌘` + `4` | 
| Instant Text/QR Recognition | `⇧` + `⌘` + `2` |
![Screenshot of Shottr’s Hotkey settings](Shottr-hotkey-settings.png)

### 3.2.4 - Velja
I use Velja to automate switching to Arc for Google apps. They are as folllows:

|Name:|**Google Docs**|
|:----|:---:|
|Open in:|Arc|
|Sample URL:|`https://docs.google.com`|
|Detect via:|Domain|
|Match:|`docs.google.com`|
|Source Apps:| <ul><li>Slack</li><li>Arc</li><li>Mail</li><li>Calendar</li></ul>|

|Name:|**Google Meet**|
|:----|:---:|
|Open in:|Arc|
|Sample URL:|`meet.google.com`|
|Detect via:|Domain|
|Match:|`meet.google.com`|
|Source Apps:|<ul><li>Notion Calendar</li><li>Rewind</li><li>Arc</li><li>Slack</li><li>Mail</li><li>Calendar</li></ul>|

|Name:| **Google Drive**|
|:----|:---:|
|Open in:|Arc|
|Sample URL:|`https://www.drive.google.com/`|
|Detect via:|Domain|
|Match:|`drive.google.com`|
|Source Apps:|`No Source Apps`|

|Name:|**Google Calendar**|
|:----|:---:|
|Open in:|Arc|
|Sample URL:|`https://calendar.google.com/`|
|Detect via:|Domain|
|Match:|`calendar.google.com`|
|Source Apps:|`No Source Apps`|

|Name:|**Jira**|
|:----|:---:|
|Open in:|Arc|
|Sample URL:|`https://atlassian.net/` 
|Detect via:|Domain|
|Match:|`atlassian.net` 
|Source Apps:|`No Source Apps`|

|Name:|**Harvest**|
|:----|:---:|
|Open in:|Arc|
|Sample URL:|`https://harvestapp.com/`|
|Detect via:|Domain|
|Match:|`harvestapp.com`|
|Source Apps:|`No Source Apps`|
| |
|Sample URL:|`https://getharvest.com/`|
|Detect via:|Domain|
|Match:|`getharvest.com`|
|Source Apps:|`No Source Apps`|

### 3.2.5 - Rocket (Emojis)
I prefer typing a `:` and searching to insert emoji. Rocket does this really well. I hide the Menu Bar icon using `Ice`.

## 3.4 - System Enhancements
### 3.4.1 - DockDoor
`DockDoor` shows you a preview of the windows you have open when you hover over them in the Dock. 

I prefer it to be clean, quick and launch on login, so I change:
In `General`:
- I check `Launch DockDoor at login`
- `Preview Window Open Delay` > `0`
- `Window Size` > `Small`
![Screenshot of DockDoor’s General settings](DockDoor-General-Settings.png)

In `Appearance`:
- `Traffic Light Buttons Visibility` > `Never visible`
![Screenshot of DockDoor’s Appearance settings](DockDoor-Appearance-Settings.png)

In `Window Switcher`:
- I uncheck `Enable Window Switcher`
![Screenshot of DockDoor’s Window Switcher settings](DockDoor-Window-Switcher-Settings.png)

### 3.4.2 - Boring Notch
`Boring Notch` is a great app and has loads of functionality to make your notch more useful on MacBooks. They added the feature I really wanted — being able to assign this to only your MacBook screen when connected to external monitors.

I think everything is fine as default, though of course I enable `Launch at login`.

## 3.5 - Utilities
These are other utilities I use that aren’t necessarily tied to system functions, but things I install, and set to open on login (they are automatically downloaded in the `packages.txt` and `mas-apps.txt`).

### 3.5.1 - AutoSwitch
I like to use AutoSwitch as secondary menu to quickly access some advanced settings. 

In `General` I set:
- `Launch:` `Launch at login` to `On`
- `Promotion:` `Show More Apps` to `Off`

In `Customisation` I turn on:
- `Hide Desktop Icons`
- `Autohide Dock`
- `Autohide Menu Bar`
- `Xcode Derived Data`
- `Show Hidden Files`
- `Empty Clipboard`
- `Show User Library Folder`
- `Show Extension Name`
- `Low Power Mode`
- `Show Finder Path Bar`
- `Screen Test & Clean`
- `True Tone`
- `Key Light`
- In here I also turn off `Hide Menu Bar Icons`

![Screenshot of OnlySwitch set up how I like it](OnlySwitch-settings.png)

### 3.5.2 - MeetingBar
I use MeetingBar only for a single function, it shows a fullscreen notification when a meeting starts, meaning I can’t ignore it. 

I therefore check `Launch after login` and `Show a fullscreen notification when event starts`.

I turn off basically everything else and hide it in my menu bar using `Ice`.

![Screenshot of my MeetingBar settings](MeetingBar-settings.png)

### 3.5.3 - Lossless Switcher
This ensures you’re always streaming the best quality when connected to AirPods or other Bluetooth headphones. In the Menu Bar, click the icon to see its settings. I like to have it in the hidden menu in `Ice` with `Show Sample Rate` selected so I can keep an eye on it.

### 3.5.4 - Amazon Q
This is a great autocomplete for Terminal, but by default it shares a lot of data with Amazon. Log in and then select the icon in the Menu Bar > `Settings`. Then under `Settings` > `Preferences` > `Advanced`, turn off `Share Amazon Q content with AWS` and `Telemetry`.

### 3.5.5 - AdGuard for Safari
I don’t generally block ads, but I prefer not to be tracked, and don’t like the popups on websites, including cookie notices. I therefore turn on:
- `Privacy`, with `AdGuard Tracking Protection filter` and `Peter Lowe's Blocklist`
- `Annoyances`, with `AdGuard Annoyances filter`

I also turn off `Show AdGuard for Safari in the menu bar`

### 3.5.6 - NepTunes
This is much better than the Last.fm app, for scrobbling. You just need to log in and grant access to your play history.

### 3.5.7 - Apparency
This is a good app to have just so you can see all the details of any app on your system in one place.

### 3.5.8 - Syntax Highlight
This is a Quick Look Extension to previewing source files using Quick Look. Another great one to have.

## 3.6 - Removing things from the Menu Bar
Loads of apps like to have Menu Bar items, and mine’s already quite cluttered, even with Ice. I therefore go into each of these apps and turn them off:
- Notion
- ChatGPT
- Figma