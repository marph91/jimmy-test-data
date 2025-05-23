## [Updating Roam](Updating%20Roam.md)
## [Change Log Archive](https://roamresearch.com/#/app/help-archive/page/dxTi-iUs2)
## **New Changes**
- [August 1st, 2023](August%201st%2C%202023.md)
    - [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md)
        - Changes to `{{video}}` `{{video-timestamp}}`
            - Video timestamps now include a block reference to the video they belong to
                - They can be dragged anywhere in Roam, and you can see all of the timestamps of a video from the linked references
                - Old video timestamps will still work, but they are not auto updated to include the block reference
            - Fixed a bug where timestamps would play a video hidden in the zoom path
            - Inserting a timestamp now automatically adds a space after the timestamp
        - Templates will now apply the state of `{{sliders}}`, `{{excalidraw}}`, `{{diagram}}` and other `{{}}` components
            - You can also now reference templates inside themselves to track the usage of them
                - Example::
                    - #roam/templates Daily mood template that tracks itself
                        - How is my mood? [*](Change%20Log.md)
                            - {{[[slider]]}}
        - When selecting a block with shift-arrow up or down, scroll the block into view
- [June 26th, 2023](June%2026th%2C%202023.md)
    - Changes to the block context menu
        - New button and key command for copying embed
            - Original button still works to copy the block ref
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FywRWXjCVNW.png?alt=media&token=630eaa4f-819e-433c-96ba-a0735c5cdb51)
- [June 20th, 2023](June%2020th%2C%202023.md)
    - [Bug Fixes](Bug%20Fixes.md)
        - Fix filtering `{{mentions}}` and `{{children-mentions}}` components
- [June 15th, 2023](June%2015th%2C%202023.md)
    - [Experimental](Experimental.md) [New Feature](New%20Feature.md)
        - `{{children-mentions: [page](roam-page://page)}}`
            - Like linked references but it also collects the linked references from all of the children blocks of `[page](roam-page://page)`. you can also use it with a block reference
- [June 12th, 2023](June%2012th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- [Performance Improvements](Performance%20Improvements.md) and new search feature for [linked references](linked%20references.md)
    - Linked references now load lazily, which means it should open *much* faster than before.
    - The downside is that you can no longer search through them with `cmd-f` or `ctrl-f`, you need to use the built in search component.
    - The new search looks through all of the references, the paths of the references, or the children if the children are open.
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F58Rma4DQAw.png?alt=media&token=542425e8-6a9d-422e-a06b-dcce8f8c1b61)
- [Roam Depot Extensions](Roam%20Depot%20Extensions.md)
## [Magic Tags](https://github.com/rcvd/magic-tags)
- Magic Tags by [Alexander Rink](Alexander%20Rink.md) transforms tags you specify into beautiful icons while maintaining all functionality, like backlinking and searching.
- ![Demo of magic tags in action](https://github.com/rcvd/magic-tags/raw/main/screenshots/magic-tags.gif)[🔗](https://github.com/rcvd/magic-tags/raw/main/screenshots/magic-tags.gif)
### How does it work
- Select the Icon Theme. [Blueprint](https://blueprintjs.com/docs/versions/3/#icons) is the default for Roam Research. Roam Studio provides [Feather Icons](https://feathericons.com/).
- Select the first magic word - this is the name of the tag (e.g., if your tag is #love, your magic word is "love")
- Select an icon from the predefined list
- Select a color from the predefined list
- Select the lightness of the color
- **Notes** You can use the same icon for multiple tags - with different colors if you like. An example of this would be a marker for high and critical tasks, which both would use the alert icon, but in yellow for high and red for critical.
- ![Settings showing tags using the same icon but different colors](https://github.com/rcvd/magic-tags/raw/main/screenshots/high-critical.png)[🔗](https://github.com/rcvd/magic-tags/raw/main/screenshots/high-critical.png)
### Feature Requests, Bugs, and Feedback
- If you need an additional icon, have an idea for a new feature, or find a bug, file it under [Issues](https://github.com/rcvd/MagicTags/issues) with a short description and a screenshot. If you have any additional comments or suggestions, please send them to [alex@goedel.io](mailto:alex@goedel.io).
### If you want to support Alex's work
- [Become a GitHub Sponsor](https://github.com/sponsors/rcvd)
- [Buy Me a Coffee](https://www.buymeacoffee.com/rcvdio)
- [Become a supporter on gödel.io](https://www.goedel.io/subscribe?utm_medium=web&utm_source=subscribe-widget&utm_content=47299057)
- [Flattr](https://flattr.com/@rcvd)
- [Paypal](https://paypal.me/rcvd)
## [roam-depot-todo-progress-bar](https://github.com/8bitgentleman/roam-depot-todo-progress-bar)
- Roam Research progress bar component for visually tracking TODOs in a list.
### Example
- ![](https://github.com/8bitgentleman/roam-depot-todo-progress-bar/raw/main/example.gif)[🔗](https://github.com/8bitgentleman/roam-depot-todo-progress-bar/raw/main/example.gif)
### Setup
- First make sure that **User code** is enabled in your settings. This allows custom components in your graph.
- ![](https://github.com/8bitgentleman/roam-depot-todo-progress-bar/raw/main/settings.png)[🔗](https://github.com/8bitgentleman/roam-depot-todo-progress-bar/raw/main/settings.png)
### Usage
- Easiest way to insert the component is though Roam's native template menu. Simply type ;; and look for **TODO Progress Bar**
- ![](https://github.com/8bitgentleman/roam-depot-todo-progress-bar/raw/main/template.png)[🔗](https://github.com/8bitgentleman/roam-depot-todo-progress-bar/raw/main/template.png)
## [oblique-strategies](https://github.com/mlava/oblique-strategies)
- Overcome creative block by using an Oblique Strategy.
- Originally create by Brian Eno and Peter Schmidt as a way to encourage lateral thinking, Oblique Strategies were originally available as a stack of cards from which you would draw a random card which held a simple prompt. See also: https://en.wikipedia.org/wiki/Oblique_Strategies for more information.
- ![image](https://user-images.githubusercontent.com/6857790/238811874-8d73b616-2bc1-49c4-89b0-f3755ed1a5a3.png)[🔗](https://user-images.githubusercontent.com/6857790/238811874-8d73b616-2bc1-49c4-89b0-f3755ed1a5a3.png)
- There have been six editions. This extension for Roam Research provides the ability to draw from any of the first five editions, or a combined list containing all of the prompts from the first five editions. The prompts were sourced from https://github.com/noaoh/oblique-stratagems with thanks.
- An Oblique Strategy prompt can be obtained using a Command Palette command or Roam Research Hotkey.
- The following commands are available:
- Random Oblique Strategy Random Oblique Strategy - 1st Edition Random Oblique Strategy - 2nd Edition Random Oblique Strategy - 3rd Edition Random Oblique Strategy - 4th Edition Random Oblique Strategy - 5th Edition
## [Roam Power Previewer](https://github.com/dragonforce2010/roam-power-previewer)
- Allows you to preview a website in a side drawer, without having to go out of Roam!
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FjnZuhSGODA.gif?alt=media&token=02e9465f-5ab4-4da7-847d-0d2f6691c23f)
- Usage
    - After installing the extension from Roam Depot, just click on a link
    - Please note that If you don't want to preview the website content in the sidedrawer or sometimes the website you are tring to preview has a iframe securty policy which forbids to do so, then you can simply press the following keys(ctrl, meta, shift) when click the link, to view the website in a new tab in browser
## [Automatic DNP](https://github.com/mlava/auto-DNP)
- Automatically paste in your preferred daily note page template when you open your DNP for the first time each day.
- This extension allows you to define templates for every day of the week, or for weekdays and weekends if you prefer to keep it simple.
- Usage
    - Use the Roam Depot settings panel to choose either Daily or Weekday/Weekend for Preferred Mode.
    - Then, paste in the block reference of a template to the corresponding fields in the Roam Depot settings screen. The example below shows the configuration for Weekday/Weekend mode:
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FDlSwEX58eB.png?alt=media&token=c4ec9f22-124c-40c8-8f0b-56b662afe774)
- [June 9th, 2023](June%209th%2C%202023.md)
    - [Bug Fixes](Bug%20Fixes.md)
        - Editing `{{excalidraw}}` drawings or `{{slider}}`s also updates the last edited time
- [June 6th, 2023](June%206th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- [Performance Improvement](Performance%20Improvement.md) to [Filters](Filters.md)
    - Opening filters is 4-5x faster
    - Adding or removing a filter is 15-30x faster
    - Memory usage is a lot less
    - This is assuming [Linked References](Linked%20References.md) is closed, because displaying all of the references is still very slow
        - We will be releasing an improvement to linked references to solve this problem soon
    - Internally we completely rewrote how these work to use the same logic as queries, so that in the future we can add OR filters
    - The counts for tags changed inside of linked refs filter
        - The counts now represent how many of the linked references have that tag. When you filter for "includes" a tag, it will show you that many references
- Small [Performance Improvement](Performance%20Improvement.md) to [Unlinked References](Unlinked%20References.md)
- Small [Performance Improvement](Performance%20Improvement.md) to [Streak](Streak.md)
- [Another](Change%20Log.md) small [Performance Improvement](Performance%20Improvement.md) to [All Pages](All%20Pages.md)
- Fixed bug that caused versions to be reordered
- Fixed old daily notes loading on scroll
    - previously it could get stuck and you would have to hover over the new note
- [May 19th, 2023](May%2019th%2C%202023.md)
    - [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
        - [Find or create page](Find%20or%20create%20page.md) performance improvement
            - Search is now 2x faster
                - Uses 1/3 of the memory of before
        - Fixed double digit numbered lists inside of the `{{search: }}` component
            - Example::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FzD-5DbE3zD.png?alt=media&token=1f7591f4-0e1c-4c22-a77a-eac822150c92)
- [May 16th, 2023](May%2016th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Big [Query](Query.md) update!
    - Queries are 2 to 10 times faster than before, depending on what you are querying for
    - Queries do not auto update by default now
        - To rerun the query, click the refresh button on the top right
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FSyeBzzxFj4.png?alt=media&token=dce1c454-ea46-4e82-85a4-e0aeb6c11571)
            - Closing and re opening the query will also rerun it
        - We made this change so that Roam doesn't get really slow when you have a query open on the page
        - If you liked how it worked before, you can change the default back to auto updating in user settings
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2Fxorb9ZSk2R.png?alt=media&token=855f684f-b57a-4545-b86e-9a324138134e)
- Delete blocks confirmation dialog
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FYDoO8C2WQa.png?alt=media&token=55f1ba57-50d1-4bbf-ba62-43550f8a8fa2)
        - Hit `enter` to confirm, or `escape` to cancel
    - You can change the threshold for when to get the warning in user settings
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FckUnHuP2ba.png?alt=media&token=c2805de1-db28-4287-93ed-701f51957aaa)
- [May 15th, 2023](May%2015th%2C%202023.md)
    - [Roam Depot Extensions](Roam%20Depot%20Extensions.md)
## [Switch+](https://github.com/dive2Pro/roam-switch-plus)
- An awesome new extension by [hyc](hyc.md) which will change the way you navigate between blocks on a page. 
- Has a number of different modes: text mode, tag mode, line mode, sidebar mode, latest changes mode. 
- Usage
    - Shortcut to activate the extension is ctrl/cmd + shift + p
Then, just start typing to search
    - You can switch modes by typing `@`, `:`, `r:` or `e:` in the beginning of the search, or you can also set hotkeys which takes you directly to a particular mode
- Do checkout the video walkthrough below:
    - <https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FzIJm0nHEOh.mp4?alt=media&token=d69cb2b5-8002-459e-9eae-08022a028f70>
- Separate GIFs demo-ing each mode
    - Text Mode
        - ![](https://user-images.githubusercontent.com/23192045/236662454-11c2ccb4-6285-41bb-b9eb-5f5232ee8275.gif)
    - Tag Mode
        - ![search with tags](https://user-images.githubusercontent.com/23192045/236662466-e5d1f2d4-7189-434b-b13b-79330a2f0082.gif)
    - Line Mode
        - ![search with line](https://user-images.githubusercontent.com/23192045/236662488-c7eca005-51cd-4bad-b781-5446b099b09c.gif)
    - Right Sidebar Mode
        - ![search with sidebar](https://user-images.githubusercontent.com/23192045/236662513-0deef455-86c9-4e98-abcf-11981e0ce805.gif)
- If you like this, you might like another one of [hyc](hyc.md)'s extensions: [Search+](https://github.com/dive2Pro/roam-search-plus). Search for it in Roam Depot!
## [Power CSS Pack](https://github.com/Roam-Research/roam-depot/pull/530)
- An extension by [Zhang Michael](Zhang%20Michael.md) which adds a lot of useful CSS classes you can use to change how a particular block in your Roam graph looks
- Usage
    - Just apply the tag you want in your block and the corresponding style will be applied. Some examples:
        - `#.css-level-bg`
        - `#.css-level-color`
        - `#.css-font-yellow`
        - `#.css-bg-olive-300`
        - `#.css-grid3`
- Check the GIF below for some examples:
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FfzFyJoIH5_.gif?alt=media&token=122ef668-6881-4489-b10f-6fb1f675de25)
## [Roam Power Themes](https://github.com/dragonforce2010/roam-power-themes)
- An extension by [Zhang Michael](Zhang%20Michael.md) with a collection of 23 beautiful themes
- ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2FExploreSpace%2FTDzPIseMY_.31.47.gif?alt=media&token=69075b59-b268-4eb7-a28e-f0ad113212d4)
- [May 10th, 2023](May%2010th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Delete button in Mobile App Quick Capture
    - [Screenshots](Screenshots.md)
- [May 9th, 2023](May%209th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Fixes for sign in via Google/Apple issues
    - Say goodbye to the dreaded "Enable Third Party Cookies to Sign up with Google" error message 🤣
- [Desktop App](Desktop%20App.md) version 0.0.18
    - Upgraded to electron 22
        - Alongside security updates and performance improvements,  enables new features like `has()` CSS selector.
    - Changed history navigation shortcuts to default browser ones (`cmd + [ / ]` in mac, `alt + left/right` in windows/linux). Old shortcuts still work too.
    - Fixes issue where forward and backward buttons in some mouses (like Logi) did not work
    - Fixes issues in Ubuntu 22.04, popOS 22.04, etc.
- Added a setting "Exportable By" via which graph owners/admins can allow/restrict users from being able to export graph data
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F6SvAKpTn3y.png?alt=media&token=fcf7e7d0-039f-4d82-9e63-d9508372a7f2)
    - Settings is under the "Sharing" tab in the settings panel
        - ... > Settings > Sharing > Exportable By
    - The default is "Anyone with access to the full graph". 
        - If the graph has not been shared with any other email and is not public, then that option is the same as "Only Me" 
- [April 21st, 2023](April%2021st%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- [More](Change%20Log.md) [Performance Improvements](Performance%20Improvements.md) to block autocomplete search
- [April 20th, 2023](April%2020th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- [Performance Improvements](Performance%20Improvements.md) to the All Pages view
- [April 17th, 2023](April%2017th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- [Performance Improvements](Performance%20Improvements.md) and [Bug Fixes](Bug%20Fixes.md) for block autocomplete search i.e. the search you get when pressing `((`
- [April 14th, 2023](April%2014th%2C%202023.md)
### [New Features](New%20Features.md) 🚀
- Tabs [block view](block%20view.md) #Experimental
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FmikHhmNdg1.png?alt=media&token=354991dc-d7c2-43fa-9f43-6c6b229a19ec)
    - If you haven't heard of block views yet
        - You can change the current block view by searching in the command palette (`cmd-p`) for "Change Block View"
            - Then type the letter of the block view you wish to use as displayed on the screen
            - You can also set a hotkey for it
        - Block views are still experimental and many parts of Roam don't work seamlessly with them yet
- [April 13th, 2023](April%2013th%2C%202023.md)
### [Excalidraw](Excalidraw.md) update
- Excalidraw is a virtual hand-drawn style whiteboard. We've now upgraded to the latest version (v0.14)
- You can create a drawing via the slash menu: `/excalidraw`
- ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F-JEizrN2ki.png?alt=media&token=4b2242fc-7063-4889-8985-26f906ca50c0)
    - above is an image so that it displays properly in older Roam clients. If you'd like to play with it, the excalidraw drawing itself is nested underneath this block
        - {{[[excalidraw]]}} {{-: Text elements in drawing: updated to latest version (v0.14) ; use via slash command: "/excalidraw" ;   Some notable upgrades ; - Supports images inside of the drawings ; - Dark mode, Canvas Background ; - Ability to resize the drawings in view mode ; - Text elements within the drawing can now be searched ; - Better pen support ; - etc }}
- Some notable upgrades
    - Supports images inside of the drawings
    - Dark mode, Canvas Background
    - Ability to resize the drawings in view mode
    - Text elements within the drawing can now be searched 
        - Works for all new drawings. For old drawings, you have to open them once in edit/fullscreen mode
    - Better pen support
    - etc
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Added JSON and JSON-LD [Code Block](Code%20Block.md) languages
- Theme Authors and [CSS](CSS.md) hackers can now target code blocks for specific languages via new CSS classes of the format `.rm-code-block--{lang}`. For example: `.rm-code-block--js` for javascript code blocks, `.rm-code-block--clj` for Clojure code blocks #CSS-Changes
    - As an example, here are the customized CSS we're using for the new JSON and JSON-LD languages (color scheme inspired from VS Code)
```css
.rm-code-block--json, .rm-code-block--json-ld {
  // colors inspired from VS Code
  .cmt-propertyName {
    color: #22509F;
  }
  .cmt-bool {
    color: #0000ff;
  }
  .cmt-number {
    color: #458A64;
  }
  .cmt-string {
    color: #95261F
  }

}

.rm-code-block--json-ld {
  // json-ld seems to use cmt-atom for booleans and cmt-meta for property names that begin with @
  .cmt-atom {
    color: #0000ff;
  }
  .cmt-meta {
    color: #22509fb6; // a lighter version of cmt-propertyName
  }
}
```
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Released fixes for issues related to [Roam Depot](Roam%20Depot.md) extensions and non-persistence of user settings
    - If you're still encountering issues after this update, please contact us at support@roamresearch.com
- [April 6th, 2023](April%206th%2C%202023.md)
    - [Roam Depot Extensions](Roam%20Depot%20Extensions.md)
## [Roam Portal](https://github.com/dkapila/Roam-Portal)
- One of the most loved Roam extensions, now available in Roam Depot!
- An easy-to-use but super-powerful search engine designed to help you explore your data visually.
- Here are just a few ideas for things you can do via this extension:
    - **Filter blocks by user:** Filter blocks modified by a particular user.
    - **View recently edited blocks:** View your recently edited blocks.
    - **Search for reactions:** Search for reactions from users. 
    - **References**: Study frequent pages and blocks mentioned in your search
    - **Time**: Analyze results over time
    - In other words, it's an easy to use
- ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FP-owbAhtRb.png?alt=media&token=078687d0-3cf1-41b1-8b8a-ca190f17ec80)
### [🔗](https://github.com/dkapila/Roam-Portal#getting-started) How to use
- After installing the extension, simply click on the Roam Portal icon located in the top right corner of the toolbar. 
- For a video tutorial on how to use Roam Portal, [click here](https://www.loom.com/share/717fa8b788844c23aa08dd7d448bf0bf).
## [Roam To SMS](https://github.com/mlava/roam-sms)
- Send SMS messages from within Roam Research!
- This extension allows you to send the contents of a block to an SMS contact using the Nexmo / Vonage API.
- ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FofvGhtact3.png?alt=media&token=5841c323-03f9-4f3e-a105-01809e77d2aa)
- [March 16th, 2023](March%2016th%2C%202023.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Fixes Roam Depot issue where "blank extensions" would appear in "Installed Extensions" section
- [March 9th, 2023](March%209th%2C%202023.md)
    - [Roam Depot Extensions](Roam%20Depot%20Extensions.md)
## [Link Preview](https://github.com/dive2Pro/roam-link-preview)
- Show brief information for external links in roam
    - ![image](https://user-images.githubusercontent.com/23192045/219956966-43781827-285d-4b66-a493-cdfdd7ea2c01.png)[🔗](https://user-images.githubusercontent.com/23192045/219956966-43781827-285d-4b66-a493-cdfdd7ea2c01.png)
    - ![image](https://user-images.githubusercontent.com/23192045/219956975-20999ad0-f2ff-4a60-8891-9ee766a7c348.png)[🔗](https://user-images.githubusercontent.com/23192045/219956975-20999ad0-f2ff-4a60-8891-9ee766a7c348.png)
## [🔗](https://github.com/dive2Pro/roam-link-preview/tree/388b5b724f6c5ddc264ac222c15b5719c9755d34#how-to-use)How to use
- You can create a custom component: link-preview with the URL as the argument
- {{link-preview https://google.com}}
    - You can write the currently copied link into Roam using a custom shortcut key
- ![image](https://user-images.githubusercontent.com/23192045/219956992-d574628e-959d-4247-be9b-b3a3d6c81e16.png)[🔗](https://user-images.githubusercontent.com/23192045/219956992-d574628e-959d-4247-be9b-b3a3d6c81e16.png)
    - You can use the context block menu to transform all links in the entire block.
- ![image](https://user-images.githubusercontent.com/23192045/223105097-8920f688-d22e-477c-af7e-461179d4dc47.png)[🔗](https://user-images.githubusercontent.com/23192045/223105097-8920f688-d22e-477c-af7e-461179d4dc47.png)
## [Quick Insert Block](https://github.com/dive2Pro/roam-quick-insert-block)
- When you need to insert a block above or below the target block , this plugin can help you reduce the number of steps.
- ![embed mode](https://user-images.githubusercontent.com/23192045/219314019-b3cd117c-81a8-4616-b251-633aac968dc6.gif)[🔗](https://user-images.githubusercontent.com/23192045/219314019-b3cd117c-81a8-4616-b251-633aac968dc6.gif)
## [Sidebar Separators](https://github.com/mlava/sidebar-separators)
- Organize your left sidebar shortcuts with separators.
- Sometimes you just want some visual separation between your list of shortcuts. This extension allows you to add a horizontal line or blank space between any of your shortcuts, so you can achieve just that.
- ![image](https://user-images.githubusercontent.com/6857790/219263679-cd1ab703-bc54-49c3-a7a0-a82016b66199.png)[🔗](https://user-images.githubusercontent.com/6857790/219263679-cd1ab703-bc54-49c3-a7a0-a82016b66199.png)
- In the above image I've inserted a horizontal line after my second shortcut and a blank line after my sixth shortcut.
- You can configure each separator in the Roam Depot settings. Use an integer to state where to insert the separator - it will be inserted after that numbered shortcut.
- You can have up to three separators, but if there's a need I'll add the option to create more.
## [Roam Depot Format Hotkeys](https://github.com/8bitgentleman/roam-depot-format-hotkeys)
- Adds hotkeys for various block formatting options including:
    - Justify Block (Left, Center, Right, Full)
    - View As Numbered List
## [Page references counter](https://github.com/fbgallet/roam-extension-ref-count)
### [🔗](https://github.com/fbgallet/roam-extension-ref-count/tree/0de3d685be89d75b62e0e99883e589ac4b62bbc8#inline-count-for-page-references-tags-and-attributes-as-superscript-like-vanilla-inline-block-reference-counter)Inline count for page references, tags and attributes as superscript (like vanilla inline block reference counter).
- 🔎 References counts are also displayed when you search for a reference, inline or in Quick search, in the autocomplete box, what is particularly useful to identify the actually used pages and the unused or wrong spellings!
- ![ref-count-v1](https://user-images.githubusercontent.com/74436347/218118672-4d7e74aa-e47f-49fb-ac95-7e59e2b1b854.gif)[🔗](https://user-images.githubusercontent.com/74436347/218118672-4d7e74aa-e47f-49fb-ac95-7e59e2b1b854.gif)
- By default, inline counts are always displayed. As an option, you can make the count appear only on hover over a given page reference. You can toggle separately inline count and search count with dedicated commands in command palette (with customizable hotkeys).
### [🔗](https://github.com/fbgallet/roam-extension-ref-count/tree/0de3d685be89d75b62e0e99883e589ac4b62bbc8#for-any-question-or-suggestion-dm-me-on-twitter-and-follow-me-to-be-informed-of-updates-and-new-extensions--fbgallet)For any question or suggestion, DM me on **Twitter** and follow me to be informed of updates and new extensions : [@fbgallet](https://twitter.com/fbgallet).
- To report some issue, follow [this link (Github)](https://github.com/fbgallet/roam-extension-stats/issues) and click on 'New issue'.
- [March 1st, 2023](March%201st%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Added Go, Markdown, and TOML [Code Block](Code%20Block.md) languages
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Fix astrolabe spinning off center
- [February 27th, 2023](February%2027th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- `#.rm-hide-for-readers` css class / tag. Hides the block and it's descendants for people who only have read access to that block. 
    - Useful for hiding a contributing guide on a public graph from those that can't edit
    - It is only a visual change ((you can still find the block in the DOM)) so don't use it to hide any secret information
- You can now sort [Roam Depot](Roam%20Depot.md) extensions by downloads, created time, updated time, or alphabetical
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FU-NrN02BGg.png?alt=media&token=15d8a284-e52e-4b10-a9f9-9cb2cdc080f1)
- [Roam Depot](Roam%20Depot.md) search improvements
    - Now it searches through authors, tags, full descriptions, and handles partial matches better
    - You can search for all the extensions by an author
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F3Kf40HxZ1Z.png?alt=media&token=c1692a8c-e61a-4dc1-8751-3e0a59da6781)
- New syntax supported in LaTeX. Now also supports [43MRmPiT2](Change%20Log.md)!
    - KaTeX (the LaTeX typesetting library we use) has been updated to the latest version, and [43MRmPiT2](Change%20Log.md) have been set up
    - (demos below will not work if Roam has not updated to the latest version. A screenshot has been attached underneath this block)
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FZB3wt0PRFV.png?alt=media&token=76a9bae9-d167-49cb-a177-d0319d6ce85c)
    - Examples of some new supported syntax
        - angl and angln
            - $$A_{\angl n} + B_{\angl g} + C_\angln$$
        - set
            - $$\Set{x \| y}$$
        - etc.
    - Macros
        - macro definition
            - these definition blocks need to be visible in order for them to be registered
            - $$\gdef\matrix#1{\begin{bmatrix}#1\end{bmatrix}}$$
                - `\gdef\matrix#1{\begin{bmatrix}#1\end{bmatrix}}`
        - katex blocks using the matrix macro defined above
            - $$
\matrix{1&2&4\\1&2&3}
$$
                - `\matrix{1&2&4\\1&2&3}`
        - [More info on using macros](https://katex.org/docs/supported.html#macros)
    - If you run into any issues with your latex blocks, please checkout the migration guide: https://katex.org/docs/migration.html
        - We're now on v0.16.4
        - If that does not resolve the issue, please contact Roam Support
- [February 17th, 2023](February%2017th%2C%202023.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Fixed the screen jump that happens when clicking into a block in the [mobile](mobile.md) app
    - Requires:: [iOS](iOS.md) 15.5 or greater (or [android](android.md))
    - **Before**
        - <https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froamteam%2FXcnjD59K61.MOV?alt=media&token=f2a52be0-21d8-4b59-b797-3985af297e4e>
    - **After**
        - <https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froamteam%2F6hyWxIeNdl.MOV?alt=media&token=7a0e5e66-ee37-46ae-9b5b-cf872c81d1a0>
- Fixed the block moving off screen when moving a block up or down on [mobile](mobile.md)
    - **Before**
        - <https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froamteam%2FlWKgJmFnLk.MOV?alt=media&token=ed03d18a-e9c3-4665-a699-1bb76cb45f7c>
    - **After**
        - <https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froamteam%2Fu9q9wrvDQ6.MOV?alt=media&token=9e71a37f-9c0b-45c5-af8d-6c2f8dc4452e>
- Fixed issues of mobile bar misbehaving
    - for example, in some devices, it would float way up and then slowly float down. In others, it would get obscured. The behavior should be much better now across the board
    - [gSwpOrALc](Change%20Log.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Filter [queries](queries.md) by the author of blocks with `{by: [user's display page](roam-page://user's display page)}`
    - You can find a user's display page title by hovering over a block they created
    - Example::
        - {{[[query]]: {and: [[Quality of Life Improvements]] {by: [[Baibhav Bista]]}}}}
- [February 14th, 2023](February%2014th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Ability to set up hotkeys for commands set up by Extensions
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F7bpy58-iBH.gif?alt=media&token=a86d51dc-b3fc-4c1c-a9c2-c45feabeaa1d)
    - Currently you might see all commands nested under "Ungrouped Extension Hotkeys". Extension-wise groupings will be available once the extension migrates to the new API (If you're an extension dev, [more here](https://roamresearch.com/#/app/developer-documentation/page/Xf6HHUsb3))
    - Video
        - <https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FsYWw81Fk4s.mp4?alt=media&token=492f1dab-db08-4d4a-a57e-be0d05dcd655>
- Expand block references in templates auto complete
    - **Before**
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FymqWiBfJcx.png?alt=media&token=5207037b-bbc8-45fc-9b13-3886207cad77)
    - **After**
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FKlF9cmZNS1.png?alt=media&token=d8a1a734-bc0d-4ea7-88fe-10b25be02095)
- Typing `"` or `'` with text selected will wrap the text with the matching character
- Pasting a link with text selected will automatically wrap the selected text with a markdown link
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FGFhJOF08A8.gif?alt=media&token=acb621be-8855-474c-b5f4-16898ef64446)
- Fix display of localhost links, i.e. http://localhost:8020/#/app/test103
    - **Before**
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F3uyFe-uWQC.png?alt=media&token=36d28887-4178-4616-aff6-2c2f5c5471cf)
    - **After**
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FabUPk7Hjhs.png?alt=media&token=5bdcc815-e409-47dc-8ecf-6f667737d0b9)
- [February 13th, 2023](February%2013th%2C%202023.md)
### [New Features](New%20Features.md) 🚀
- `cmd-f` / `ctrl-f` find in page search for the [Desktop App](Desktop%20App.md) (version `0.0.16` or higher)
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FgUXDFC3iyv.gif?alt=media&token=48f93162-7116-4c7d-a325-f630cac5d16c)
- [February 11th, 2023](February%2011th%2C%202023.md)
### [New Features](New%20Features.md) 🚀
- Streak 
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FcGQgqUSI84.png?alt=media&token=d386efe3-ea41-46e4-92e6-c08d06428683)
        - got this via `{{[[streak]]: [[Daily Highlight]]}}`
    - Provide it a reference to one or more pages or blocks, it will generate a heatmap showing how often that ref pattern appeared in your daily notes. 
    - Click any cell to open matching blocks in the sidebar
    - use via `/streak`
    - you can pass in a single page, or pass in multiple pages, or even pass in query-type syntax!
        - examples
            - `[[DONE]]`
            - `{{[[streak]]: [[DONE]] [[Solutions]]}}`
            - `{{[[streak]]: {or: [[DONE]] [[Solutions]]}}}`
    - [Conor White-Sullivan](Conor%20White-Sullivan.md)'s tweet
        - https://twitter.com/Conaw/status/1624154783560142848
- [February 8th, 2023](February%208th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Multi-select move block up / down (Mac: `cmd-shift-up/down`, PC: `alt-shift-up/down`)
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FbibqCXYQLm.gif?alt=media&token=0c4f7e85-8b2c-418a-8017-1b42154ed0d9)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- [mobile](mobile.md) [iOS](iOS.md) Fix sync issues that would sometimes appear when reinstating app from background
    - [android](android.md) version did not have this issue but will be receiving an update as well in the next few days
### [New Features](New%20Features.md) 🚀
- Open search in sidebar (alt-enter or opt-enter)
    - <https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F5_JZnrFS-l.mp4?alt=media&token=b6bfe09e-14f3-42af-be58-02bb6a2fffbc>
    - One can also use the slash command for a persistent search view (i.e. type `/search`)
- [February 7th, 2023](February%207th%2C%202023.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- If global filters are applied on the log, then show the filter icon so you can remove them
- [February 1st, 2023](February%201st%2C%202023.md)
    - [Roam Depot Extensions](Roam%20Depot%20Extensions.md)
## [Self-Destructing Blocks](https://github.com/8bitgentleman/roam-depot-block-self-destruct)
- Set blocks to self-destruct (be deleted) after a period of time. Every hour the plugin will search for all blocks that reference #self-destruct (configurable to whatever you would like). Any of those references that are older than the time set will be deleted.
- A custom deletion time can be set by nesting an attribute below the block that you want deleted.
### [🔗](https://github.com/8bitgentleman/roam-depot-block-self-destruct#use-case-ideas)Use Case Ideas
- Blocks left over from daily templates
- Using queries on your Daily Notes page or old queries in general.
- Keeping your graph lean and clean
### [🔗](https://github.com/8bitgentleman/roam-depot-block-self-destruct#examples)Examples
- ![](https://github.com/8bitgentleman/roam-depot-block-self-destruct/raw/main/example.png)[🔗](https://github.com/8bitgentleman/roam-depot-block-self-destruct/raw/main/example.png)
## [Hide Topbar Buttons](https://github.com/mlava/hide-topbar-buttons)
- Reduce unneccessary clutter!
- This extension allows you to take control of the appearance of your Roam Research topbar. You can choose to show or hide default Roam Research buttons in the topbar.
- ![image](https://user-images.githubusercontent.com/6857790/213940140-67f212c2-596f-4771-a92a-e5519136a80a.png)[🔗](https://user-images.githubusercontent.com/6857790/213940140-67f212c2-596f-4771-a92a-e5519136a80a.png)
- In the topbar you can choose to hide:
    - Page Filter button
    - Calendar button
    - Three Dot menu button
    - Page Width button
    - Help button
    - Right Sidebar button
- You can select to Hide on Mobile or Hide on All Platforms. This means you can have different settings for different purposes.
- For example, if you want to hide the Help button on mobile only but hide the Calendar button on all platforms, just select Hide on Mobile for Help and Hide on All Platforms for Calendar.
- TODO:
    - allow buttons from Roam Depot extensions to be hidden
## [Augmented Headings](https://github.com/mlava/augmented-headings)
- Add H4, H5 and H6 headings to your Roam Research graph!
- With this extension, you can create H4-H6 headings and control their CSS very easily. Simply install the extension and then modify the settings in Roam Depot. Note that if you don't change the font settings in Roam Depot settings you won't see any change in the text output even if you make that block a heading. You **must** set font settings to see any difference.
- **New:**
    - added setting to allow user-configured heading tags. If you don't want #h4 you could use #.h4 or even #purple_elephant for that heading tag, and the extension will handle it.
- The new headings even work with my Sticky Headings and Table of Contents extension as well!
- ![image](https://user-images.githubusercontent.com/6857790/214956832-d2711867-ab73-4af0-9e29-074eaf0b3ac8.png)[🔗](https://user-images.githubusercontent.com/6857790/214956832-d2711867-ab73-4af0-9e29-074eaf0b3ac8.png)
- For each heading level you can configure:
    - font size
    - font weight
    - font style
    - font variant
- You can set a heading using the Command Palette. Click into a block and then select 'Toggle Heading - H4', 'Toggle Heading - H5' or 'Toggle Heading - H6'. Or, right click on the block bullet, go to Plugins and then select the Toggle commands from there.
- If your heading is H4 and you click to toggle H4, it will return to normal text. This is how Roam handles H1-H3. However, if you toggle to a different heading level (e.g. H4 -> H5) it will overwrite to the new level. Again, this is how Roam handles this case.
- [January 31st, 2023](January%2031st%2C%202023.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Fix plaintext paste (`ctrl-shift-v`) pasting twice on desktop app in linux and windows
- [Roam Depot Extensions](Roam%20Depot%20Extensions.md)
## [Roam Website Title Parser](https://github.com/dragonforce2010/roam-website-title-parser)
- This extension can parse the website title and transform the link to the markdown format when you paste a url into roam block
- For example, when you paste a link like this `https://developer.roamjs.com/`, this extension is gonna transform it to `[Introduction - RoamJS](https://developer.roamjs.com/)`
- [January 30th, 2023](January%2030th%2C%202023.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Fix Chinese language autocomplete not working in top level blocks in references
- Fix Chinese language showing the incorrect word count in all pages
- [January 24th, 2023](January%2024th%2C%202023.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Fix drag and drop on [android](android.md)
- [December 20th, 2022](December%2020th%2C%202022.md)
    - Fixes a couple of performance issues, should be noticeable especially for [Local Graph](Local%20Graph.md)s
- [November 30th, 2022](November%2030th%2C%202022.md)
    - [Roam Depot Extensions](Roam%20Depot%20Extensions.md)
## Roam reference expands
- show the path of the block reference
- ![](https://github.com/dive2Pro/roam-reference-expand/raw/49e028ae09c5ec50eeec4436bd81247b7a7e0685/SCR-20221124-d9c.png)
- ![](https://github.com/dive2Pro/roam-reference-expand/raw/master/reference%20extends.gif)
# Uninstall
- All configurations are stored on the [roam/reference extends/config](roam_reference%20extends_config.md) page and need to be removed manually if you want to uninstall the plugin cleanly.
## Mapbox
- Render interactive maps directly in your graph!
## Usage
- Type `{{maps}}` in a block. When the block renders, an interactive map will render in its place!
- To position the map at a particular center, create a child block with text "Center". Under that block, put in the latitude and longitude coordinates of the center delimited by a comma.
- To start the map at a particular zoom level, create a child block with text "Zoom". Under that block, put in the zoom level value which should be a number. A minimum value of 0 is zoomed all the way out and a maximum value of 18 is zoomed all the way in.
- To add Markers to the map, create a child block with text "Markers". Under that block, add one child for every marker you want to include. In the block, write the text you'd like as the label of the block. As a child of **that** block, put the latitude and longitude coordinates of the marker.
- For example, the following configuration will have to be set as the child of the block to produce the map below:
    - Center
        - 32.715736, -117.161087
    - Zoom
        - 12
    - Markers
        - David Vargas
            - 32.7, -117.2
        - RoamJS
            - 32.72, -117.1
- If the Marker text is already a tag in your graph, clicking on the marker pin will take you to that page. Shift clicking the marker will open the tag in the sidebar.
- You could also filter the markers that are displayed on your map. Clicking the wrench icon on the top right will open the settings overlay, where you could specify a tag to filter by. All markers that are pages that have a block with the entered tag will remain on the map while the rest get filtered out.
- [November 29th, 2022](November%2029th%2C%202022.md)
    - [Roam Depot Extensions](Roam%20Depot%20Extensions.md)
## Oura Ring
- Import your Oura Ring daily summaries on a given day into your daily note page!
## [🔗](https://github.com/dvargas92495/roamjs-oura-ring#usage)Usage
- You'll first need to add your personal access token associated with your Oura Ring account to the Token field in your Roam Depot Settings. The extension needs this in order to access your personal data. [Click here](https://cloud.ouraring.com/personal-access-tokens), to generate your own personal access token.
- To import your Oura Ring data to your daily note page, open the Command Palette and enter "Import Oura Ring". If the current page is a Daily note page, it will query the day before the page title, since you usually want to track last night's sleep. Otherwise, it will query yesterday's data by default. It will output the following text:
```javascript
Bedtime Start:: hh:mm:ss
Bedtime End:: hh:mm:ss
Sleep Duration:: hh:mm:ss
Total Sleep:: hh:mm:ss
Total Awake:: hh:mm:ss
Light Sleep:: hh:mm:ss
Rem Sleep:: hh:mm:ss
Deep Sleep:: hh:mm:ss
Day Start:: hh:mm:ss
Day End:: hh:mm:ss
Low Activity:: hh:mm:ss
Medium Activity:: hh:mm:ss
High Activity:: hh:mm:ss
Rest Activity:: hh:mm:ss
Readiness Score:: hh:mm:ss
```
- You can also import the data by creating a button by typing `{{import oura ring}}` into a page and clicking the button.
## Roam native dark theme
- ![](https://github.com/dive2Pro/roam-native-dark/raw/master/SCR-20221120-hek.png)[🔗](https://github.com/dive2Pro/roam-native-dark/blob/master/SCR-20221120-hek.png)
- ![](https://github.com/dive2Pro/roam-native-dark/raw/master/SCR-20221120-hfj.png)[🔗](https://github.com/dive2Pro/roam-native-dark/blob/master/SCR-20221120-hfj.png)
- [November 28th, 2022](November%2028th%2C%202022.md)
    - [Roam Depot Extensions](Roam%20Depot%20Extensions.md)
## SamePage
- Official Roam client into [SamePage](https://samepage.network/) - the intra tool-for-thought protocol.
- Use SamePage to connect your Roam Graph to other notebooks to sync changes across them, perform cross notebook queries, and more! To get started, install this extension and request an invite code by emailing [support@samepage.network](mailto:support@samepage.network). Check out our docs at https://samepage.network/docs!
## WARNING
- The SamePage family of extensions are still **in beta** and are not considered stable yet for real or sensitive data. All data shared on SamePage is considered public and probability of data loss is high.
- Previously, extensions were not listed on the change log, please check out our [github](https://github.com/Roam-Research/roam-depot) for a [full list of new extensions and updates](https://github.com/Roam-Research/roam-depot/pulls?q=is%3Apr+is%3Aclosed). From now on, all new extensions will be listed here
- [November 11th, 2022](November%2011th%2C%202022.md)
    - Small fixes
        - Fixes issue on restore graph from EDN where some graphs would get stuck near completion
        - Fixes "Roam was not built in a day" error that would arise sometimes when collapsing right sidebar windows corresponding to pages
- [October 6th, 2022](October%206th%2C%202022.md)
    - [New Features](New%20Features.md)
        - Single Block Multiselect Mode
            - Select blocks but not their children or select non consecutive blocks and perform bulk actions on them
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FCtabMYCHRV.png?alt=media&token=2ff14e70-6c2c-4e3b-8dc0-318966366c07)
            - **How to use**
                - Toggle the mode on / off with `ctrl-m` (PC) or `cmd-m` (Mac) (customizable)
                - Then click a checkbox to select it
                - Shift click another checkbox to select a range between that checkbox and the last one selected
            - **Available commands**
                - Drag and dropping blocks
                - Right click context menu
                    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FhmG851Z2bl.png?alt=media&token=f2366b67-bd41-4e3c-b373-46bbee59f956)
            - This feature is still a work in progress.
                - Key commands (tab, shift-tab etc) do not work with it
### More of [2022](2022.md)
- [September 30th, 2022](September%2030th%2C%202022.md)
    - Small fix: if a window already exists in the sidebar and it is tried to open again, it jumps up to the top of the sidebar
    - A number of changes throughout the last week for integration of write actions with the new backend API
        - [Developer Notes](Developer%20Notes.md): Checkout [Roam Backend API (Beta) docs](https://roamresearch.com/#/app/developer-documentation/page/W4Po8pcHQ). 
            - New addition: [Write actions](https://roamresearch.com/#/app/developer-documentation/page/J-hxpYKmK)
- [September 7th, 2022](September%207th%2C%202022.md)
    - [New Features](New%20Features.md)  #Improvements
        - [Blueprint Color](https://blueprintjs.com/docs/versions/3/#core/colors) palettes for code blocks (these colors match what is used in Roam)
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FtBmBkVpT0d.png?alt=media&token=35ab4556-dbd5-4694-9621-63a726147657)
    - #Quality-of-Life-Improvements #Bug-Fixes
        - Fixed checkbox alignment on [Firefox](Firefox.md)
            - **Before**
                - ![Screenshot 2022-09-07 at 17 57 57](https://user-images.githubusercontent.com/285292/188948053-ba930d81-6bc4-4de9-8d13-d0fe9acc01f5.png)
            - **After**
                - ![Screenshot 2022-09-07 at 17 58 16](https://user-images.githubusercontent.com/285292/188948064-96cd01d0-6822-4294-b3fb-19462121368a.png)
- [August 18th, 2022](August%2018th%2C%202022.md)
    - [New Features](New%20Features.md) *sort of* #Tag-Styles
        - We decided to include some of the most useful [roam/css](roam_css.md) [Tag Styles](Tag%20Styles.md) we've developed for ourselves, you may find helpful/inspiring [FmhjiXgxA](Change%20Log.md) [tY2Q6q3Oo](Change%20Log.md) and [fbGyeCJOo](Change%20Log.md)
## .rm-E 
- Behavior::
    - Blocks tagged with `#.rm-E` will display their immediate children next to them, 
        - rather than indented below them
- Use Cases::
    - When you want a sort of [Mind Map](Mind%20Map.md) light behavior, 
        - or just want to view things side by side
    - 🤷‍♂️ it's nice to have when you want it not much more to it than that
- Example::
    - A #.rm-E 
        - B
            - Note that this only impacts the first level of nesting
        - C
            - If you want to go further, you have to keep using the tag
        - D [.rm-E](.rm-E.md)
            - Using the link, not the tag
            - so you can see where it is used
            - E [.rm-E](.rm-E.md) 
                -  since this class hides itself when used as a tag
## .rm-g 
- Behavior::
    - Blocks tagged with `#.rm-g` are hidden when they are open  - revealing the children nested within them 
        - Children are styled to look like they are one level higher in the block hiearchy than they are -- useful for adding meta-data tags without visually cluttering your outline.
- Use Cases::
    - when you want to group a collection of items and hide the block that contains them
- Example::
    - [.rm-g](.rm-g.md) #Fruits 
        - Apples
        - Pears
        - Cherries
## .rm-hide
- Use Cases::
    - When you want to add some info to a block without visually cluttering things up - but still allow the info to be discoverable easily
- Behavior::
    - This block only displays when it is open - when it is closed, it is replaced with a very light bar across it's length
        - The bar get's darker on hover, and which
            - when you click it - it opens the block
    - In some ways a mirror of [tY2Q6q3Oo](Change%20Log.md) 
- Example::
    - [x] This is a task that I'm hiding the metadata for
        - Total Time:: 2 min #.rm-hide  
            - Start time:: 17:26
            - End time:: 17:28  
    - The block above me ((((jq0MYtn5U)))) has a hidden child - hover between us and click the bar to expand it - or arrow key up from me, or down from it, and you'll see it
        - Have some hidden children here too
        - #.rm-hide 
            - hidden children
        - Look between us!
    - [CSS Changes](CSS%20Changes.md)
        - Zooming out from sidebar, embed-path, or backlinks now outlines the block you were originally focused on, rather than coloring the block and all it's children with an obnoxious yellow
            - Example::
                - Shift click on this reference [aD4jjcDOt](Change%20Log.md) and then click a breadcrumb in the sidebar and 
                    - you'll see this  ->  ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FKfjpSlNswz.png?alt=media&token=7ab3240d-5f22-4292-b0d0-6ca3d217b115)
        - Images now display inline (previously the forced a line break)
        - References of blockquotes and Images now display inline
            - Now it is easier to use them for building up compound statements
                - Example::
                    - > All Men are Mortal
                    - > Socrates is a Man
                    - > Socrates is Mortal
                    - > [IF](IF.md) ((rECUGYx_U)) [AND](AND.md) [rvlquM4gT](Change%20Log.md) 
[THEN](THEN.md) [aD4jjcDOt](Change%20Log.md)
- [August 17th, 2022](August%2017th%2C%202022.md)
    - [New Features](New%20Features.md)  #Improvements
        - [Latex](Latex.md) now will parse block references, including other latex so you can comp
            - Example::
                - $$[86cQzNJhR](Change%20Log.md)[Civl1vpd2](Change%20Log.md) + [eswTPC4el](Change%20Log.md) [5XDZIpbeU](Change%20Log.md) $$
### Recursive Latex
- $$\frac{[he0H9MCmU](Change%20Log.md)}{[8YUhtbFfK](Change%20Log.md)}$$
    - $$n_1$$
    - $$n^n$$
### Plain Text
- \sum_{[f32673rdf](Change%20Log.md)}[qEPfTMWSO](Change%20Log.md)
    - ^z
    - i=1
### Reference of Reference - to describe how variable used in another context
- $$\mapsto [LvGTzNBu3](Change%20Log.md)$$
    - Here you can describe the meaning of mapsto n^n
    - [8YUhtbFfK](Change%20Log.md)
        - Here you could describe the meaning of the n^n that is being described here
### Sizing
- \Large
    - Try changing [86cQzNJhR](Change%20Log.md) to 
        - \Huge
        - \Small
            - Use Cases::
                - Being able to separately describe each element of the equation.
    - #Quality-of-Life-Improvements #Bug-Fixes **[Feature Behavior Change](Feature%20Behavior%20Change.md)**
        - Behavior of [Inline Calculator](Inline%20Calculator.md) `{{calc: }}` for parsing block references has changed 
            - [Old State](Old%20State.md)
                - Previously, when you composed calculations across many blocks - all of the math text was pulled up and flattened - which could lead to unexpected behavior when building up statements and making calculations that depended on other calculations 
                    - Example::
                        - Wait? 2 times 4 doesn't equal 5! ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FeoLoaSY0y_.png?alt=media&token=0fb80ad2-894a-40b5-ba87-841b7fa3cd63)
                            - After Change:: [evPly3KEV](Change%20Log.md)
                    - The old hack to get around required you to wrap block references in a `( )` to make sure that that each component in the calculation was evaluated independently before the values were aggregated  ((748osab9-)) remember [PEMDAS](PEMDAS.md)?
                        - This is what is actually being evaluated now - if you're using lots of nested refs  ((5R-4pOGOe))
            - [New State](New%20State.md)
                - After this update, every reference used in a calculation will be wrapped in a `()` automatically before calculation is applied
                    - Example::
                        - 2 times 4 = 8  ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FC500DSjbn0.png?alt=media&token=5ea62b8f-f710-4e59-ba20-b7d4e25c474e)
                            - [Try it here](Change%20Log.md)
                    - 2 times 20 = 40, not 21
                        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froamteam%2FZCxS2W-TvQ.png?alt=media&token=64cd1702-a33f-4517-b198-ebad16f9836c)
                - New Features::
                    - Clicking the green text of the [calc](calc.md) function has always displayed content of the internals of the calcuation, but now if you click on the = sign after doing this, you can see the fully expanded function which is being evaluated, so you can confirm that everything is happening the way you want it to 
                        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FvIZpt-B0OI.png?alt=media&token=a87650f5-0fcc-46c0-a31a-2231b01f9d6d)
                        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F0QAGtWb2NP.png?alt=media&token=f7821d1a-5834-45bc-99c0-6240757cffcd)
                        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F_0bfRasZfz.png?alt=media&token=edd56c7d-6590-44be-92e3-4b187a50fad2)
## Try it yourself
- [Z](Z.md) {{[calc](calc.md): [9VZ6lwlfx](Change%20Log.md) * [zqspvHH4e](Change%20Log.md)}}
    - [X](X.md) {{calc: [pJOOIdwKC](Change%20Log.md) + [U35nxx0ha](Change%20Log.md)}}
        - 1
        - 1
    - [Y](Y.md) {{calc: [xdm0aDOmu](Change%20Log.md) + [k9UaJrwOM](Change%20Log.md)}}
        - 2
        - 2
- [August 15th, 2022](August%2015th%2C%202022.md)
    - [New Features](New%20Features.md) #Alpha
        - `{{embed-path: ((block-ref))}}` - Experimental new view of block embeds where path is visible and clickable - similar to what you'd see for the block in inline-references 
            - [Problem it Solves](Problem%20it%20Solves.md)
                - Often when viewing embeds, it is frustrating to not be able to see the context of the embed - the embed-path component lets you see the parent path of the block at a glance, and navigate to it quickly.
    - #CSS-Changes
        - Changed the styling when you zoom out of a block in a context - like sidebar and moved the color into a css variable 
            - `var(--inline-highlight-color)` for the color of ==highlights==
            - `var(--highlight-color)` for color of highlighted blocks due to zooming out in a embedded context like within backlinks, sidebar, or block refs.
- [August 11th, 2022](August%2011th%2C%202022.md)
    - [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md)
        - Search field to help you find the graph you want to switch to d
            -  in sidebar 
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FXqRHzdD9g9.png?alt=media&token=307c2373-aee6-4cc4-8321-8926a2aa7faa)
            - on all-graphs page
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FZldEt56a8N.png?alt=media&token=9f6292f0-3ec2-4117-8359-dae3760063ab)
        - Update to the help database to remove custom styling
-  [July 25th, 2022](July%2025th%2C%202022.md)
    - [Roam Depot](Roam%20Depot.md) #Plugins
        - [PhonetoNote](PhonetoNote.md)
            - Create a dedicated phone number to send and forward messages to a Roam graph + more
                - https://twitter.com/phonetonote/status/1551764556707397633?s=20&t=qEEBfrUN4jkSq9qSt5HDAQ
-  [July 19th, 2022](July%2019th%2C%202022.md)
    - [Roam Depot](Roam%20Depot.md) #Plugins 
        -  [Matter](Matter.md) 
            -  great way to sync highlights
            - https://twitter.com/matter/status/1549490849595080704?s=20&t=qEEBfrUN4jkSq9qSt5HDAQ
- [July 15th, 2022](July%2015th%2C%202022.md)
    - #New-Features [Roam Depot](Roam%20Depot.md) #Major-Launch
        - https://twitter.com/RoamResearch/status/1547823281478066177?s=20&t=qEEBfrUN4jkSq9qSt5HDAQ
    - [Roam Depot](Roam%20Depot.md) #Plugins 
        - [Bionic Text](Bionic%20Text.md)
            - https://twitter.com/fbgallet/status/1548083399977340930?s=20&t=qEEBfrUN4jkSq9qSt5HDAQ
- [July 11th, 2022](July%2011th%2C%202022.md)
    - Fixed backspace deleting selected blocks when opening up the command pallete
        - Also added refocusing of the selected block when hitting `escape` to exit the command pallete
    - Increase markdown import limit from 10 to 10,000
- [June 24th, 2022](June%2024th%2C%202022.md)
    - [mobile](mobile.md)
        - [iOS](iOS.md)
            - Fixed tab, shift-tab, backspace, and arrow keys on ipad with an external keyboard
            - Fixed sign in flash on app restart
            - Fixed saving the last used graph across app restarts
        - [android](android.md)
            - Fixed back gesture
            - Added native Google and Apple sign in
            - Added sign out
- [June 15th, 2022](June%2015th%2C%202022.md)
    - [mobile](mobile.md) [iOS](iOS.md)
        - Apple sign in
        - Native google sign in
        - Fixed sharing text with newlines in it
        - Password Manager autofill for login/password
- [June 12th, 2022](June%2012th%2C%202022.md)
    - [Desktop App](Desktop%20App.md) Links
        - Requires [updating](Updating%20Roam.md) the desktop app to `0.0.15`
        - Deep links that allow one to directly navigate to a graph/page/block in the desktop app
        - Demo video (showing some convenient usage tricks too)
            - <https://www.loom.com/share/fb5095868df041a597712b7403c87ed4>
        - URL Format
            - Similar format to normal Roam web links
                - instead of `https://roamresearch.com/` we have `roam://`
            - Example
                - Roam web link: `https://roamresearch.com/#/app/help/page/hyL5OPFah`
                - Desktop app link: `roam://#/app/help/page/hyL5OPFah`
- [June 6th, 2022](June%206th%2C%202022.md)
    - Sign in with Apple
    - Report this page for public graphs
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F_F1M_ESBjE.png?alt=media&token=3b062277-b461-4c1d-877e-260f53017f5c)
- [June 3rd, 2022](June%203rd%2C%202022.md)
    - Fixed bug with namespaces not showing correctly
        - introduced yesterday in [3XkUpjpkP](Change%20Log.md)
- [June 2nd, 2022](June%202nd%2C%202022.md)
    - Fixed bug with changing the code block language
        - introduced by [parsing change](Change%20Log.md)
    - Keep original block first in ordering of inline refs
    - Password reset emails now use app.roamresearch.com
- [May 25th, 2022](May%2025th%2C%202022.md)
    - Fix the parsing of bold in italics and italics in bold (and highlight and strikethrough). It no longer matters what order you put them in.
        - Examples::
            - `***^^bih^^***`: ***^^bih^^***
            - `***^^ibh^^***`: ***^^ibh^^***
            - `**==__bhi__==**`: **==__bhi__==**
            - `***^^ibh^^***`: ***^^ibh^^***
            - `==**__hbi__**==`: ==**__hbi__**==
            - `***^^bih^^***`: ***^^bih^^***
    - Small improvement to all pages search ((Longer debounce time and normalize the search value))
- [May 23rd, 2022](May%2023rd%2C%202022.md)
    - Fix [mobile](mobile.md) quick capture crashing when displaying old quick captures
- [May 9th, 2022](May%209th%2C%202022.md)
    - Fixed [mobile](mobile.md) quick capture page auto complete results
- [April 4th, 2022](April%204th%2C%202022.md)
    - Added the ability to remove email-password login if you are also signed in with Google
- [April 3rd, 2022](April%203rd%2C%202022.md)
# **Mobile App**
- The Roam mobile app is now available for download on the [iOS](https://apps.apple.com/us/app/roam-mobile/id1609277273) (iphone and ipad) and [android](https://play.google.com/store/apps/details?id=com.roamresearch.relemma&hl=en_US&gl=US) app stores
- [March 10th, 2022](March%2010th%2C%202022.md)
    - Performance improvement to opening pages with a large amount of mentions while the mentions are closed (~4x faster for a page with 6.1k mentions)
        - Note that this does not improve the performance of actually opening the mentions
- [March 8th, 2022](March%208th%2C%202022.md)
    - [Code Block](Code%20Block.md)
        - [Solidiity](Solidiity.md) syntax highlighting support
        - Fixed issue with color picker showing on the `constructor` keyword
- [March 3rd, 2022](March%203rd%2C%202022.md)
    - Fixes "All Pages" view so that all columns (Word Count, Mentions, Updated, etc) can be seen when searched
        - (was a CSS bug introduced some time ago)
- [February 16th, 2022](February%2016th%2C%202022.md)
    - Apple Silicon (M1) [Desktop App](Desktop%20App.md)
        - Do you need to install the new App?
            - First [check if you are using a new M1 Mac](https://www.howtogeek.com/706226/how-to-check-if-your-mac-is-using-an-intel-or-apple-silicon-processor/)
            - If you are using an M1 Mac, then you should install the new app
                - It will be much faster than the old one
        - See [our migration guide](FAQ.md) for how to migrate from our old (intel) desktop app to the new (Apple Silicon) one
- [February 12th, 2022](February%2012th%2C%202022.md)
    - Initial load memory and performance updates, related to [fl5hlmHWj](Change%20Log.md)
        - You may experience a longer load time on while your graph upgrades, you should see a message like this
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FlgY6E66Azc.png?alt=media&token=99a2a6c2-1fd2-4dc5-a6a9-53a1bc45fb53)
        - [Technical Details](Technical%20Details.md)
            - Loading from Roam's servers
                - up to 50% faster
                - up to 66% less peak memory usage (during load)
                - up to 20% reduction in idle memory usage (after app loads)
            - Loading from Indexeddb (local)
                - up to 16% faster
                - up to 40% less peak memory usage (during load)
                - up to 20% reduction in idle memory usage (after app loads)
                - up to 33% reduction in used disk space
            - https://www.loom.com/share/824de8dbd66c40e591eac1404e66198e
- [February 11th, 2022](February%2011th%2C%202022.md)
    - Fix having to double click to edit text on [iOS](iOS.md) [Safari](Safari.md)
        - Before
            - <https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FMgQBi2FROY.MP4?alt=media&token=10254893-b682-4a78-94e5-3ec85d632f1a>
        - After
            - <https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FXbMOzNrxpu.MP4?alt=media&token=42386235-418c-42a3-9b4c-5e6699a5cf0e>
- [February 9th, 2022](February%209th%2C%202022.md)
    - Fixed bug selecting multiple blocks in embeds and linked references
- [February 7th, 2022](February%207th%2C%202022.md)
    - Update datascript to `1.3.9` [*](Change%20Log.md) [*](Change%20Log.md)
        - Includes [performance improvements](https://github.com/tonsky/datascript/blob/master/CHANGELOG.md#130) that might make extensions faster
    - Bug fixes related to [fl5hlmHWj](Change%20Log.md)
        - Delayed full release of load performance improvements
    - Fixed potential memory leak
    - Bug fixes to our update / upgrade mechanism
- [February 3rd, 2022](February%203rd%2C%202022.md)
    - Prevent clicking out of [Import](Import.md) while files are importing
        - Also added text showing progress, similar to EDN restore
    - Change [Encrypted Graphs](Encrypted%20Graphs.md) password
        - In the settings panel
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FJ6QeY8K-Zf.png?alt=media&token=2eb6670a-49b7-4696-b35d-0a2d06357815)
    - Fix paste bug causing images to be pasted instead of text from Microsoft Word
    - Revert [wBT317GzU](Change%20Log.md)
        - Unfortunately had a bug that broke some extensions, will re release as soon as the bug is fixed
- [February 1st, 2022](February%201st%2C%202022.md)
    - Add icon to encrypted graphs in all graphs view
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FnyXbh-I1p-.png?alt=media&token=28305988-ec3d-40df-a6fb-68da45ee5609)
    - Update datascript to `1.3.8`
        - Includes [performance improvements](https://github.com/tonsky/datascript/blob/master/CHANGELOG.md#130) that might make extensions faster
    - Fix bug with [Restore](Restore.md) graph, causing some data to not be imported correctly
    - Fix not [Export](Export.md)ing `:log/id`, causing daily note pages to not show up in the log
- [January 29th, 2022](January%2029th%2C%202022.md)
    - [Encrypted Graphs](Encrypted%20Graphs.md)
    - Unlimited graphs for all
    - Increase upload file size from 100MB to 500MB
- [January 28th, 2022](January%2028th%2C%202022.md)
    - Preparation work for graph load / memory improvements (stay tuned)
    - Small additions to the roamAlphaAPI (see docs [here](https://roamresearch.com/#/app/developer-documentation/page/tIaOPdXCj) for detailed changelog)
- [January 25th, 2022](January%2025th%2C%202022.md)
    - [Import](Import.md)
        - Small speed / memory improvements
        - Bug fix causing import to fail when importing a large amount of files
- [January 3rd, 2022](January%203rd%2C%202022.md)
    - A major change and some minor additions to `roamAlphaAPI`, the API that roam extensions are built on top of.
        - If you're a dev or are interested, more details [here](https://roamresearch.com/#/app/developer-documentation/page/tIaOPdXCj)
### [2021](2021.md)
- [December 7th, 2021](December%207th%2C%202021.md)
    - [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md)
        - Better error checking for queries
            - fixed bug where queries could previously lead to "Roam was not built in a day" errors 
        - [Performance Improvements](Performance%20Improvements.md) for imports and queries
- [November 26th, 2021](November%2026th%2C%202021.md)
    - [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md)
        - Fix upload issues in [iOS](iOS.md) 
        - Automatic handling of snapshot issues
- [November 17th, 2021](November%2017th%2C%202021.md)
    - Natural Language Date suggestions now work in "Find or Create Page" search bar
        -  Example screenshot
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FM37NPNdNsm.png?alt=media&token=90e32ba6-8c10-4cca-8ddc-ff78d605c8b0)
- [November 10th, 2021](November%2010th%2C%202021.md)
    - Natural Language Dates
        - You can now write dates in natural language in Roam.
        - Write the date in square brackets  in any format, and Roam will convert it to a date.  
        - Select the suggested date for it to be entered in your block. 
        - **Example Screenshot**
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FVzRPrXeIeH.png?alt=media&token=2173eb04-fd27-43e0-b1ca-cce79de3efde)
        - Some other examples you might want to try
            - `[5 days ago](roam-page://5 days ago)`
            - `[2 weeks from now](roam-page://2 weeks from now)`
            - `[last friday](roam-page://last friday)`
            - `[wed](roam-page://wed)`
            - `[2021-11-13](roam-page://2021-11-13)`
            - `[11-13-2021](roam-page://11-13-2021)`
            - `[17 nov 2019](roam-page://17 nov 2019)`
- [November 9th, 2021](November%209th%2C%202021.md)
    - [Code Block](Code%20Block.md) [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md)
        - Updated to `codemirror.next`
            - Performance for large code blocks should be significantly better
        - Styling changes
            - **before**
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2Fzf8iKJxhjd.png?alt=media&token=840a48fc-71ce-4252-a6c7-d98ad3d85d3f)
            - **after**
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FVbqMOAbS_G.png?alt=media&token=0b5230ad-1701-4728-bf97-19d6fe45ee04)
                - 
        - Added `latex` and `dart` languages
        - Added collapsable code gutters
        - Added highlighting matching brackets
        - Changed the default font to [fira code](https://github.com/tonsky/FiraCode)
        - Added line wrapping
            - [Example](Example.md)
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F7wwZFV60hs.png?alt=media&token=5c951c49-c9b4-4385-b2ac-30663b6d4b32)
- [November 5th, 2021](November%205th%2C%202021.md)
    - [Bug Fixes](Bug%20Fixes.md) - fix errant text insertion for [Firefox](Firefox.md) tab change
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FBBUiFSsRHb.png?alt=media&token=1a30076d-4afd-441e-9fea-311bbcfce4bb)
- [October 12th, 2021](October%2012th%2C%202021.md)
    - Major [Performance Improvements](Performance%20Improvements.md) to filters on pages and backlinks 
        - Should be particularly noticeable on huge collections - like TODO pages or user display name pages in multiplayer graphs.
- [October 7th, 2021](October%207th%2C%202021.md)
    - [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md)
        - Fix [autocomplete](autocomplete.md) appearing offscreen in [embed](embed.md)s, the [Right Sidebar](Right%20Sidebar.md) and [mobile](mobile.md)
            - [embed](embed.md)
                - **before**
                    - Autocomplete gets "trapped" inside of the embed
                    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2Fl-yBff_stw.png?alt=media&token=72683948-7ebc-440c-8bd6-0e34aff4a8bd)
                    - and scrolls the embed, which sometimes leads to the embed getting stuck
                        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FVobJ470b9-.png?alt=media&token=1d4a2e9a-9b1e-401f-8182-12b962a5bfb0)
                - **after**
                    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froamteam%2FdfjnNdt-Xv.png?alt=media&token=6a134550-fb43-4035-bfb3-fa5fdc74f840)
            - [Right Sidebar](Right%20Sidebar.md)
                - **before**
                    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2F0jSiiGlMdB.png?alt=media&token=b1a96c21-c829-411c-b49b-bc3d51833fa7)
                    - also sometimes led to a similar issue [as with embeds](Change%20Log.md), where the sidebar got stuck offscreen
                - **after**
                    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FI8GsnHl0hB.png?alt=media&token=c7a6d654-5135-4168-8f4f-c88d6ae9993f)
            - [mobile](mobile.md)
                - **before**
                    - Autocomplete causes the whole screen to scroll to the right
                        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2Fj5Gk-J5ayh.png?alt=media&token=e6246ae0-ebdc-4fe2-9283-522f0f22be1e)
                - **after**
                    - Autocomplete adjusts to fit the size of the screen
                        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FPBNQMc-v1S.png?alt=media&token=c977b686-2179-4627-8324-55867e264010)
- [September 28th, 2021](September%2028th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- All settings, including keyboard shortcut customizations accessible from [Command Palette](Command%20Palette.md) 
    - `cmd-p` on [Mac](Mac.md)
    - `control-p` on [Windows](Windows.md) or [Linux](Linux.md)
    - *handy way to discover or remember different keyboard shortcuts*
    - Example::
        - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FBykG_v_8KV.png?alt=media&token=76c76dce-6346-4b6e-9435-843f07219956)
- [September 27th, 2021](September%2027th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Added a shortcut (`Cmd/Ctrl+Opt+R`) to toggle [Youtube](Youtube.md) [Videos](Videos.md) playback while typing in a block
- Made [Video Timestamps](Video%20Timestamps.md) look a little nicer
### [Bug Fixes](Bug%20Fixes.md)  🛠
- Fixed bug that caused Roam to crash when [Query](Query.md) using `between` contained only one date
- [September 21st, 2021](September%2021st%2C%202021.md)
    - [Customization](Customization.md) #End-User-Programming #Quality-of-Life-Improvements
        - Custom components in [JSX](JSX.md) and [Javascript](Javascript.md)
        - <https://grain.co/highlight/NkzVPjnoX3P8gavWAVq9g00DiABYGCE1gWZIU63J>
        - [Example](Example.md)
            - <https://grain.co/highlight/2xiEAKKj5It1deDSFzbwWMbm3JXLwqt0OdtzmQ53>
- [September 18th, 2021](September%2018th%2C%202021.md)
    - [Customization](Customization.md) [Improvements](Improvements.md)
        - Styling changes applied to blocks via `#.style-tags-like-this` now propogate to references of those blocks [inARykipE](Change%20Log.md), ((yFVz-h6iu)) and [oWJOFygKp](Change%20Log.md)
            - white
            - blue #.bg-blue-500 #.text-white 
            - red #.bg-red-500  #.text-white 
        - Propogates many levels up too -- see ((((q_CXURfgB)))) 
- [August 26th, 2021](August%2026th%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md)  🛠
- Fixed bug where when opening references of a block in the sidebar, two instances would show up
- Fixed issues around Display Name not showing
### [Developer Notes](Developer%20Notes.md) 🧑‍💻 
- Fixed bug for removing window via front-end API
- Fixed bug for opening mentions in sidebar via front-end API
- [August 11th, 2021](August%2011th%2C%202021.md)
### [New Features](New%20Features.md) 🚀
- You can now use [Video Timestamps](Video%20Timestamps.md) for Youtube videos!
- Either type `/video timestamp` or hit `Cmd/Ctrl+Alt+t` under a video to enter a timestamp
- Example::
    - <https://www.youtube.com/watch?v=4yXK9OMc2OU>
        - 00:07:07 
            - #Notes Cmd+U opens search bar 
            - 00:07:08
            - 00:07:08
            - 00:08:57
            - 00:09:02
            - 00:09:43
            - 00:09:45
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Fixed [Mobile Menu Bar](Mobile%20Menu%20Bar.md) to insert double brackets instead of single brackets
- [August 3rd, 2021](August%203rd%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md)  🛠
- Fixed bug with image links containing `\r`
- [July 11th, 2021](July%2011th%2C%202021.md)
### [New Features](New%20Features.md) 🚀
- You can now change your sign in email inside the new `Account` panel in the `Settings` menu
- [July 8th, 2021](July%208th%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠 
- Fixed bug where cursor remained did not move to the end of the generated template content
- Fixed bug where inline css would get loaded before styling from `roam/css`
- Minor bug fixes and improvements.
### [Developer Notes](Developer%20Notes.md) 🧑‍💻 
- `data.block.create` and `data.block.update` can now be used to set alignment,  heading, and the children blocks' view type. See [developer docs](https://roamresearch.com/#/app/developer-documentation/page/CAtB5a7wv) for more info.
- [June 23rd, 2021](June%2023rd%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Slash menu () will only trigger when the slash is at the very beginning of a block, or preceded by a space - *not* in the middle of a word
- [June 11th, 2021](June%2011th%2C%202021.md)
### [New Features](New%20Features.md) 🚀
- Desktop app for macOS, Linux, and Windows is out now!
    - Download from the `...` menu in the top right of your screen, the [Graphs and Settings](Graphs%20and%20Settings.md) page, or [our home page](https://roamresearch.com)
- [June 9th, 2021](June%209th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Much faster load times when opening a graph
- [June 8th, 2021](June%208th%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠 
- Fixed some bugs around auto-backups, graph deletion, file manager
- [June 4th, 2021](June%204th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- [Date picker](Date%20picker.md)
    - Made it much faster
    - You can now change first day of week and see the week number
        - Go to `Settings > User Settings > International` to toggle.
    - Improved styling
        - {{[[table]]}}
            - Before
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FsfZWPjD0QC.png?alt=media&token=553e5c25-9bb5-43c1-8a1e-b2081810cce3)
            - After
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2FQTG7J8YQV-.png?alt=media&token=d637b2c6-157f-4d2d-a810-cf0c9e1fb5f7)
        - 
- [June 2nd, 2021](June%202nd%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- You can now copy a [Block References](Block%20References.md) while editing it (via `Cmd/Ctrl+Shift+C`)
- You can now see other references inline for [Block References](Block%20References.md). Go to `Settings > User Settings > Inline Reference Counts` to activate.
### [Bug Fixes](Bug%20Fixes.md) 🛠 
- Fixed plaintext paste in [Safari](Safari.md)
- [May 25th, 2021](May%2025th%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠 
- Reverted [GIS4PCuUD](Change%20Log.md)
- Comment button will no longer keep showing up after taking screenshots or switching apps
- Made date picker faster
- Fixed pasting multiple blocks multiple times
### [New Features](New%20Features.md) 🚀 #.h
- Added support for [Kroki](Kroki.md) diagrams ([Link](https://kroki.io)) #.h
    - How it works::
        - Write your kroki code in a code/regular block, for instance,
```plain text
graph TD
  A[ Anyone ] -->|Can help | B( Go to github.com/yuzutech/kroki )
  B --> C{ How to contribute? }
  C --> D[ Reporting bugs ]
  C --> E[ Sharing ideas ]
  C --> F[ Advocating ]
```
        - Then use the following syntax
            - `{{[kroki](roam-page://kroki): TYPE_HERE: BLOCK_REF_HERE}}`
                - so for instance, `mermaid:((13fZ8yxDr))` will produce:
                    - mermaid:((13fZ8yxDr))
    - Screenshots::
        - ![](https://camo.githubusercontent.com/a4f4453e86abb6804f9f92ca477e8be856653aad9571ad62b728b22ee4e0634a/68747470733a2f2f666972656261736573746f726167652e676f6f676c65617069732e636f6d2f76302f622f666972657363726970742d35373761322e61707073706f742e636f6d2f6f2f696d6773253246617070253246726f616d2d7465616d253246682d65424e786637314a2e706e673f616c743d6d6564696126746f6b656e3d31386662333735362d336163372d346262362d616363612d393166333562626638633432)
- [May 17th, 2021](May%2017th%2C%202021.md)
### [New Features](New%20Features.md) 🚀
- You can now quickly jump to/between [Daily Notes](Daily%20Notes.md) pages using the date picker!
    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Fhelp%2Fy0yYV8dNw_.png?alt=media&token=df5b78f9-3a25-4a8c-8b7c-3eed0dba191e)
- Open graph-view for page has been moved into the dropdown menu
- [Secret Feature](Secret%20Feature.md) - to be announced after round on testing
- [May 16th, 2021](May%2016th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- [Pages](Pages.md) [Sharing](Sharing.md) has been re-introduced
- [Query](Query.md) will load 50 results at a time ((to prevent humongous queries from freezing Roam))
- [Query](Query.md) results can now be grouped by pages
- You can now show/hide paths of blocks in [Query](Query.md) results
### [Developer Notes](Developer%20Notes.md) 🧑‍💻 
- Added `data-uid` to [Block References](Block%20References.md)
- [May 12th, 2021](May%2012th%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠 
- Long-pressing the expand/collapse button will expand all blocks in linked references, like in normal blocks.
- Fixed PDFs not rendering
- [May 7th, 2021](May%207th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Block embeds will now be expanded by default
- [May 4th, 2021](May%204th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- You can now shift-click breadcrumbs/path of zoomed-in block to open in [Right Sidebar](Right%20Sidebar.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠 
- Made [Query](Query.md) and [Linked References](Linked%20References.md) slightly faster
- Pasting blocks containing images will no longer destroy block structure
- Made text highlights legible in [Block References](Block%20References.md) previews
### [Developer Notes](Developer%20Notes.md) 🧑‍💻
- iFrame Components are a new possibility for extending Roam. Write components using any JS framework, host it on your own server, but interact with Roam graph data. Documentation https://roamresearch.com/#/app/developer-documentation/page/YNgZSgVSS.
- [May 3rd, 2021](May%203rd%2C%202021.md)
### [New Features](New%20Features.md) 🚀
- Hidden feature for [Roam Team](Roam%20Team.md)'s internal use, will be notifying believers if no bugs in next few days, and rest of the community shortly after that.
- [April 30th, 2021](April%2030th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Added syntax highlighting for [SPARQL](SPARQL.md) and [Turtle](Turtle.md) #.Kifah
### [Developer Notes](Developer%20Notes.md) 🧑‍💻
- As part of our ongoing effort to keep Roam secure, we're improving how extension settings are stored. **Please review your roam/js, roam/css and Custom Components settings and re-enable the ones you want to use again. **
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Auto-backups will no longer trigger when you switch/reload your graph.
- The block info pop-up will no longer show up while dragging blocks on [Safari](Safari.md)
- Fixed a bug with graph settings not appearing on local graphs
- [April 29th, 2021](April%2029th%2C%202021.md)
### [New Features](New%20Features.md) 🚀
- You can now easily manage/delete all your uploaded files by going to `... > Settings > Files`
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Pasted HTML links/images whose URL contains brackets will no longer break [Alias](Alias.md). Go ahead, paste that [Wikipedia](Wikipedia.md) page!
- Prevent creating orphaned blocks on backspace
### [Developer Notes](Developer%20Notes.md) 🧑‍💻
- Moved `data-edit-time`, `data-create-time`, and `data-edit-display-name` from `span.rm-bullet` to `div.rm-block`
- Added `data-edit-photo-url`
- So now we can style the entire block easily based on who wrote it and access the users' profile photo url if they have one from signing in with google ((and in the future all users when we allow custom profile pictures))
- [April 28th, 2021](April%2028th%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Fixed bug which created orphan blocks when deleting in [Linked References](Linked%20References.md)
- [April 23rd, 2021](April%2023rd%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Contents of [Kanban](Kanban.md) will now load normally when its children are collapsed
- Pressing Enter will split the Kanban card instead of inserting an empty card
- Cards can be deleted or joined like in normal blocks
- Some components like images will no longer overflow the kanban
- Disabled vertical scrolling on the [Mobile Menu Bar](Mobile%20Menu%20Bar.md)
- Minor performance improvements
- [April 22nd, 2021](April%2022nd%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Fixed performance regression
- Made settings modal mobile-friendly.
- [April 21st, 2021](April%2021st%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Added buttons for undo, redo, square+round brackets to the mobile menu bar!
### [Bug Fixes](Bug%20Fixes.md) 🛠 
- Cursor will be placed correctly when adding TODO via the mobile menu bar
- Multibar lines will no longer show over the mobile menu bar
- [April 20th, 2021](April%2020th%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠 
- Fixed Graph Settings not opening and removed sharing tab for [Local Graph](Local%20Graph.md)
- [April 18th, 2021](April%2018th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Improved dropdown menu 
- Moved Sharing settings into its own tab
### [Bug Fixes](Bug%20Fixes.md) 🛠 
- Redo will now work more than once
- [April 16th, 2021](April%2016th%2C%202021.md)
### [New Features](New%20Features.md) 🚀 
- Custom shortcuts! You can find them in `Settings > Hotkeys`
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- You can now hide code blocks in search results. To toggle, go to `Settings > User Settings`.
- User Settings and Graph Settings have been unified into the new Settings modal.
### [Bug Fixes](Bug%20Fixes.md) 🛠 
- Empty `<a>` (link) tags in pasted content will no longer be rendered.
- [April 15th, 2021](April%2015th%2C%202021.md)
### [New Features](New%20Features.md) 🚀
- Unlimited [local graphs](Local%20Graph.md) are now available for all Roam subscribers!
- [April 14th, 2021](April%2014th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Hitting tab while writing a page reference will autocomplete the first option
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Fixed an embed styling issue
- [April 12th, 2021](April%2012th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Added [Elixir](Elixir.md) as a code block option
- [April 9th, 2021](April%209th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md)
- Page width is now persisted
- [April 7th, 2021](April%207th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Improved mobile menu bar and replaced Drawing helper button with [TODO](TODO.md) button
    - {{[[kanban]]}}
        - Before::
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2F6Xk2JBlhBF.png?alt=media&token=4da2b9c2-37de-405d-98a9-212b0f5cdffe)
        - After::
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2F6Yjwj-4gvL.png?alt=media&token=ff977aec-d135-4caa-9f76-3edf05a9b570)
- **UI Updates**
    - Cleaned up the [Left Sidebar](Left%20Sidebar.md)
        - {{[[table]]}}
            - Before::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FArTNrMYLgt.png?alt=media&token=c0a5d24c-b242-410c-a1a9-029a7638ac88)
            - After::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FCMTzJVwz0x.png?alt=media&token=fc77ed41-c550-4859-a13b-791d0962132b)
    - Cleaned up [Quick Capture](Quick%20Capture.md)
        - {{[[kanban]]}}
            - Before::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FiY8WCjeeTO.png?alt=media&token=b2da9700-7c0b-42f6-8b07-4e3dd4e20f41)
            - After::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2Feuu53BSFc4.png?alt=media&token=14a8ee81-8ea0-4439-ac74-2129804b2917)
    - Revamped Import modal
        - {{[[table]]}}
            - Before::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FSX7k6To7rD.png?alt=media&token=4056c63d-e4ba-4bec-a978-dfcefac1dcc9)

            - After::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FkXpJm3dgXf.png?alt=media&token=7cd87887-93d4-4c41-8952-db82777e1117)
        - {{[[table]]}}
            - Before::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FbMLzO7q-5M.png?alt=media&token=d3fb0597-9eab-4c3d-a9f0-8ff72ab2f086)

            - After::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FItNe6Dk54D.png?alt=media&token=116c8d07-837a-43f6-9020-a0e9b23f9fe1)
    - Updated Sharing settings
        - {{[[table]]}}
            - Before::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FuWcVSPMzHQ.png?alt=media&token=fd0ca15c-03e6-49c6-91f4-3bc352450dbc)
            - After::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2F6sPn5_q0gs.png?alt=media&token=74e2fa98-7488-4729-b0e8-7b664692aa79)
        - And with the page sharing security warning:
            - {{[[table]]}}
                - Before::
                    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2F5JbnowYACh.png?alt=media&token=886f3455-154f-4c9c-b5da-8ce127517675)
                - After::
                    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FkzwI4ilx0f.png?alt=media&token=14985bc9-daaa-474d-91d1-8511632b8dbf)
        - The sharing options:
            - {{[[table]]}}
                - Before::
                    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2F1Nz_WX-5rJ.png?alt=media&token=1e9f9b67-22b6-43c2-b244-beee49393e46)
                - After::
                    - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FgKV0seo2nF.png?alt=media&token=61a7206b-6dd5-4ccd-b7c3-429e6dff7522)
    - Lighter Roam bullets, slightly thinner bold text, and subtler multibar so you can focus on your content
        - {{[[table]]}}
            - Before::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2F6mUQuhMfeY.png?alt=media&token=3e46c965-ad22-45a5-ba51-4fce71a60283)
            - After::
                - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FOWqQH4AWhh.png?alt=media&token=c19e6e1e-ca64-4a30-b4c3-35b0e4177deb)
- [April 6th, 2021](April%206th%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- **Kanbans are now directly editable**
    - Navigate around with key commands (cmd-<arrow> on Mac)
    - Relocate cards with key commands (cmd-shift-<arrow> on Mac)
    - Reorder with drag n' drop
    - Drag and drop blocks in and out of the kanban with more precise location control
    - Edit cards in the kanban
    - Enter adds a card below and focuses it
    - Click in a column to add a card
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Minor performance improvements
- [April 5th, 2021](April%205th%2C%202021.md)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Fixed a memory leak and improved performance
- [April 2nd, 2021](April%202nd%2C%202021.md)
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Added shortcut hint in context menu for copying [Block References](Block%20References.md)
- Made it clearer that deleting a graph doesn't immediately allow using its name again
    - {{[[table]]}}
        - Before::
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2F5j3PFaZ5Xz.png?alt=media&token=6d36fc43-b6bc-434d-98fa-22250b6416c9)
        - After::
            - ![](https://firebasestorage.googleapis.com/v0/b/firescript-577a2.appspot.com/o/imgs%2Fapp%2Froam-team%2FkDgsAI3wOK.png?alt=media&token=07e6f288-00dd-4a03-ac21-1d10ea038f3d)
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Update Changelog link in `Check for Updates` toast
- [March 30th, 2021](March%2030th%2C%202021.md)
### [New Features](New%20Features.md) 🚀
- You can now export the block you're zoomed into instead of the whole page
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- Block embeds are now resolved to text in [Markdown](Markdown.md) exports
- Added an icon to easily access the right sidebar
    - The shorcuts icon has been turned into an option inside the ... dropdown menu
- Added better visual feedback for adding/removing shortcuts
### [Bug Fixes](Bug%20Fixes.md) 🛠
- Strikethrough and redo shortcuts on Windows have been reverted to Win+Y and Ctrl+Y respectively following reports that users couldn't redo more than once.
- [March 28th, 2021](March%2028th%2C%202021.md)
### [New Features](New%20Features.md) 🚀
- You can now export in [Flattened Markdown](Flattened%20Markdown.md), which removes all indentation and block formatting
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨
- [Block Embed](Block%20Embed.md)s will remember whether you closed or opened them between page reloads
- When editing a page title, any preceding/trailing whitespaces will be automatically removed
- When exporting a single [page](Pages.md), you'll directly receive the exported file instead of a zipped file.
- [March 24th, 2021](March%2024th%2C%202021.md)
### [New Features](New%20Features.md) 🚀 
- New Help Graph!
### [Quality of Life Improvements](Quality%20of%20Life%20Improvements.md) ✨ 
- Added warning banner to experimental graphs 
- [roam/comments](roam_comments.md)
- [May 11th, 2023](May%2011th%2C%202023.md)
    - [Baibhav Bista](Baibhav%20Bista.md)
        - ((_7JKQRlnF))
            - If anyone is curious how I got the two images side by side, open the command palette (cmd-p) and then "Change block view". The one I'm using here is "horizontal"
                - If you use these block views regularly, might want to set a hotkey for it. That can be done via the command palette as well
- [February 2nd, 2022](February%202nd%2C%202022.md)
    - [Joshua Brown](Joshua%20Brown.md)
        - ((knVAQbuR-))
            - * not for beta users