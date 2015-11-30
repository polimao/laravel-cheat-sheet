# Sublime Text Cheat Sheets Plugin
Cheat Sheets is a plugin for quickly accessing cheat sheets in the Sublime Text editor. Typing the key sequence will open a cheat sheet in a new tab. If the cheat sheet is already open, it will activate that tab.

![Regular Expressions Cheatsheet](https://raw.github.com/dmikalova/sublime-cheat-sheets/master/example.png "Regular Expressions Cheatsheet")

## Installation
### Package Control
The [Cheat Sheets package](https://sublime.wbond.net/packages/Cheat%20Sheets) is available in [Package Control](https://sublime.wbond.net/installation). Once Package Control is installed, install Cheat Sheets by opening the command palette `Ctrl + Shft + P`, type **Install**, and select **Package Control: Install Package**, then type and select **Cheat Sheets**.

### Clone from Github
```
git clone https://github.com/dmikalova/sublime-cheat-sheets.git
```

## Available Cheat Sheets
At the moment most cheat sheets are under heavy development. Feel free to submit your own sheets or edits. Be aware that edits to the defaults sheets will be erased by an update. If you want to safely edit a sheet, copy it from `$ST/Packages/Cheat Sheets/cheat-sheets` to `$ST/Packages/User/cheat-sheets`. If both folders have sheets with the same $filename then the one in `$ST/User/cheat-sheets` will be opened.

Cheat Sheets can be opened either from the menu: `Tools > Cheat Sheets`, the command palette by pressing `Ctrl + Shft + P` and typing Cheat Sheet, or from the following keyboard shortcuts:

Command                    | Keyboard Shortcut
-------------------------- | -----------------
Bash *                     | Ctrl + Shft + C,  S, H
Git *                      | Ctrl + Shft + C,  G, I, T
Github Flavored Markdown * | Ctrl + Shft + C,  G, F, M
Go *                       | Ctrl + Shft + C,  G, O
KDE *                      | Ctrl + Shft + C,  K, D, E
Regular Expressions        | Ctrl + Shft + C,  R, X
Sublime Text *             | Ctrl + Shft + C,  S, T
\* Incomplete sheet.

## How to add your own Cheat Sheets
1. Add your cheat sheet to `$ST/Packages/User/cheat-sheets/$filename.cheatsheet`.

2. Add a keyboard shortcut by adding the following line to `$ST/Packages/User/Default ($OS).sublime-keymap` and change the keys and $filename:
	```json
	[
		{ "keys": ["ctrl+shift+c", "n", "s"], "command": "cheat_sheet", "args": {"cheatsheet": "$filename"} }
	]
	```

3. Add a menu entry by adding the following to `$ST/Packages/User/Main.sublime-menu` and change both instances of $filename:
	```json
	[
		{ "id": "tools", "children": [
			{ "id": "cheat-sheets", "caption": "Cheat Sheets", "children": [
				{ "caption": "$filename", "command": "cheat_sheet", "args": {"cheatsheet": "$filename"} }
			]}
		]}
	]
	```

4. Add a palette item to `$ST/Packages/User/Default.sublime-commands` and change both instances of $filename.
	```json
	[
		{ "caption": "Cheat Sheet: $filename", "command": "cheat_sheet", "args": {"cheatsheet": "$filename"} }
	]
	```

	To add multiple cheat sheets copy and paste just the keys or caption line and add a comma in between each entry to all the above files.

5. Highlighting follows this format:
	```
	>\t Header
	>\t\t Subtext
	Text
	Command \t Text
	Command \s\s Text
	\tCommand \t Text # Comments
	```

	Where \t means tab and \s means space.

* If there's a problem, you can use the cheat_sheet_tester command. The tester command will print in the console the file paths where it expected to find your $filename. The console can be opened with `` Ctrl + ` `` or `View > Show Console`.

	The tester command can be run directly in the console with:
	```python
	view.run_command("cheat_sheet_tester", {"cheatsheet": "$filename"})
	```

	The tester command can also be run as a keyboard shortcut with:
	```json
	{ "keys": ["ctrl+shift+c", "r", "y"], "command": "cheat_sheet_tester", "args": {"cheatsheet": "$filename"} }
	```

## External Programs
If you want to have access to your cheat sheets outside of Sublime Text you can use [KLook](http://www.koryavov.net/2012/03/klook-new-utility-for-kde-and-rosa.html) on KDE, [Gloobus](http://gloobus.net/gloobus-preview/) on Gnome, [Quick Look](http://www.macworld.com/article/1131923/qlterminal.html) on OSX, or [maComfort](http://rafaelklaus.com/macomfort/) on Windows. However none of the these have syntax highlighting, and there's always the `subl` command to quickly open a file in Sublime Text.

## Credits
This plugin is based off of Steve Hammond's [Cheater](https://github.com/shammond42/cheater) plugin.