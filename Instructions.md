_by Keith Kranker, (originally posted on [my site](http://econweb.umd.edu/~kranker/code), moved to this page May 2010)_

# Introduction #

[Notepad++](http://notepad-plus-plus.org) (on [sourceforge](http://notepad-plus.sourceforge.net)) is currently my favorite because it is so easy to add literally any computer language or modify how they are displayed. Here's a screenshot of a Stata .do file:

![http://notepad-stats-integration.googlecode.com/files/statafromnotepad%2B%2B.png](http://notepad-stats-integration.googlecode.com/files/statafromnotepad%2B%2B.png)

Adding colors, underlining, and so makes the code much easier to stare at.  It also help check your code since "replase" won't be highlighted but "replace" will.  It also allows the enhancements many text editors offer: tabbed file viewing, saved sessions, and all that jazz.

Great! But what's this stuff for? When you are in Notepad++, editing your latest .do or .ado file and want to try out the code: if you've followed these directions, you can just hit the F8 or F9 button on your keyboard and send the file to Stata.

_Note:  If you want to run files in [batch mode](http://www.stata.com/support/faqs/win/batch.html), you don't need to do ANY of this. See my note below._

# Credits #

This is posted simply to add to [Friedrich Huebler's excellent page](http://huebler.info/2005/20050310_Stata_editor.html) explaining how to pass files into Stata. These are just a few notes on how to (only slightly) tweak the code for use with [Notepad++](http://notepad-plus.sourceforge.net/).  Friedrich Huebler deserves _full credit_ for the code. I simply tweaked the code for this particular application. (after a little time to figure out AutoIt). The only reason worth posting this page is for a few comments.

There was also a  [Statalist post](http://www.hsph.harvard.edu/cgi-bin/lwgate/STATALIST/archives/statalist.0608/date/article-886.html) from Jeffrey Arnold with some modifications of Huebler's code. The advantage is that the script feeds the commands into Stata via a text file (instead of cutting & pasting it in).  This is the approach I use below.  It also uses an .ini file to control program names.

The programs posted below are mostly composed of a verbatim combination of these scripts.  I give full credit to them for the "heavy lifting."

# Download files #

All my files can be downloaded by clicking on the **[source](http://code.google.com/p/notepad-stats-integration/source/browse/)** tab above, then browsing through the files.  There is a "download raw file" link to the right of the pages.

# Steps to run with Notepad++ #

1.  If you haven't installed [Notepad++](http://notepad-plus.sourceforge.net/), do so first.

2. In principle, you can download the scripts from [Friedrich Huebler's page](http://huebler.info/2005/20050310_Stata_editor.html) can be dowloaded an installed as-is, using his directions and a little guidance from below.  However, I have changed the code somewhat, (see "Credits" above) and therefore recommend downloading the files listed under the Source tab (above).  Download them all into the same folder.

3. Edit the .ini file to match your installation of Stata.  You will need to change the `StataExe` and `StataWin` keys.

4. Use AutoIt to compile these scripts. [Huebler](http://huebler.info/2005/20050310_Stata_editor.html) provides detailed instructions. In short, this amounts to downloading and installing Autoit, open the .au3 files, and hitting Ctrl+F7 on your keyboard.  In the same folder as your .au3 files, you will now find .exe files of the same filename.

5. Use Notepad++'s "Run" capability to run your script file.

  * Find the `shortcuts.xml` file for your installation of Notepad ++

  * Open this file with a different text editor (not Notepad++) or "trick" Notepad++ by following [these instructions](https://sourceforge.net/apps/mediawiki/notepad-plus/index.php?title=Configuration_File_Editing)

  * Insert the following lines of text:
```
<Command name="Stata: Do Current File" Ctrl="no" Alt="no" Shift="no" Key="120">
	&quot;C:\{your filepath}\SEND2STATA.KAK.EXE&quot; do &quot;$(FULL_CURRENT_PATH)&quot;</Command>

<Command name="Stata: Include Current File" Ctrl="no" Alt="no" Shift="no" Key="120">
	&quot;C:\{your filepath}\SEND2STATA.KAK.EXE&quot; include &quot;$(FULL_CURRENT_PATH)&quot;</Command>

<Command name="Stata: Run Current File" Ctrl="no" Alt="no" Shift="no" Key="120">
	&quot;C:\{your filepath}\SEND2STATA.KAK.EXE&quot; run &quot;$(FULL_CURRENT_PATH)&quot;</Command>

<Command name="Stata: Run Selected Text" Ctrl="no" Alt="no" Shift="no" Key="119">
	&quot;C:\{your filepath}\RUNDOLINES.KAK.EXE&quot;</Command>

<Command name="Stata: Help for selected text" Ctrl="yes" Alt="no" Shift="no" Key="119">
	&quot;C:\{your filepath}\HELPDOLINES.KAK.EXE&quot;</Command> 

```

  * These directives assign the Autoit programs to Shortcut Keys in Notepad++.  The first line uses **F9** (`Key="120"`).  You will need to choose something else if (1) you want another key than I or (2) the keys I chose are already assigned to something else in your copy of Notepad ++ (i.e., in _Settings_ / _Shortcut Mapper_)

  * While you're at it, you might want to also add the shortcuts for Stata Batch Mode, Stat-Trasnfer, SAS etc...  (discussed below)

  * Obviously, replace `{your filepath`} above with the actual filepath to your new .exe files.  The quotation marks to surround the filepaths as `&quot;`.  These will be replaced (by Notepad++) with actual quotes.

  * The shortcuts.xml file is often `C:\Documents and Settings\{Windows User Name}\Application Data\Notepad++\` in Windows XP  or `C:\Users\{Windows User Name}\AppData\Roaming\Notepad++ ` in Windows Vista. You should be able to find it by typing the following address into Windows Explorer: `%APPDATA%\Notepad++`

  * After saving `shortcuts.xml`, you will need to restart Notepad++.

  * Notepad++'s menus only get updated when Notepad starts up, so this restarting step is important.

  * The use of `$(FULL_CURRENT_PATH)` is explained in the [wiki](http://sourceforge.net/apps/mediawiki/notepad-plus/index.php?title=Category:Short_Title(All)).

6. It should now work:
  * Hit **F9** to run the .do or .ado file in Notepad++

  * Select some text, hit **F8** to run selected text in the current Stata window (via a temporary text file and the `include` command)

  * Select a word, hit **Ctrl+F8** to look up the word in Stata's help menu.

> Note:  Some people seem to be having trouble with the F8 button.  If so, open Notepad++ and go to _Settings_, _Shortcut Mapper_.  Make sure that you do not already have F8 assigned to something else.  This is a problem with the latest versions of Notepad++.

7. Add your own custom syntax highlighting for .do and .ado files.
  * In Notepad++, go to View,  User Define Dialog...

  * Then, set up syntax highlighting according to your own preferences.

  * Hint: in Stata, use the command `net search getcmds` since it's not part of the Stata package. Then, run the command. Next simply cut and paste everything from the output file into one of the boxes on the "Keywords List" tab.

  * The [source files](http://code.google.com/p/notepad-stats-integration/source/browse/) contain several potential versions of `userDefineLang.xml` file for Stata (versions 9 and 11).

  * Notepad++'s menus only get updated when Notepad starts up and a .do file only gets assigned to to the Stata syntax highlighting when it is loaded.  So, if you changed some of the settings, you will need to either (1) close your .do file and reopen (or "reload" from the file menu) and/or (2) close and reopen Notepad++.

8. You can use a similar process to set up [Auto-Completion](http://sourceforge.net/apps/mediawiki/notepad-plus/index.php?title=Auto_Completion).  [Here](http://sourceforge.net/apps/mediawiki/notepad-plus/index.php?title=Editing_Configuration_Files#Autocompletion.2C_aka_API.2C_files) are instructions for editing the file. The [download package](http://code.google.com/p/notepad-stats-integration/source/browse/) contains a file named `Stata.xml`, which can be used to get you started.  You drop the file into `plugins\APIs` in the Notepad++ Installation Folder.

### Other Notepad++ Help ###

  1. For (1) general information about text editors and Stata and (2) directions about syntax highlighting with Notepad++ for Stata .do and .ado files: check out [this page](http://fmwww.bc.edu/repec/bocode/t/textEditors.html#notepadplus)
  1. Following recommendations from [this page](http://fmwww.bc.edu/repec/bocode/t/textEditors.html) ,
  1. I found it useful to tweak Stata to add shortcuts to Notepad++. See the files `npp.ado`, `npp.hlp`, and `npp.do.profile.do` (code to add to your profile.do file)
  1. Notepad++ [wiki articles](http://sourceforge.net/apps/mediawiki/notepad-plus/index.php?title=Category:Short_Title(All)) are hard to find, but contain great nuggets of information.

# Other Programs #

### Stata in Batch Mode ###

If you want to run files in [batch mode](http://www.stata.com/support/faqs/win/batch.html), you don't need to do ANY of the instructions above.  You can skip AutoIt, and everything else and just create shortcut in the "RUN" menu to execute something similar to the following:
```
  "C:\Program Files\Stata9\wstata.exe" /e do "C:\my folder\my file"
```

Therefore, the run menu would need an entry like this:
```
<Command name="Stata: Batch Mode" Ctrl="no" Alt="no" Shift="no" Key="121">
	cmd /c cd &quot;$(CURRENT_DIRECTORY)&quot; &amp;&amp; 
	&quot;C:\Program Files\Stata9\wstata.exe&quot; /e do &quot;$(FULL_CURRENT_PATH)&quot;</Command>
```

Above, I used Windows' `CMD.exe` to execute two commands instead of one.  I change the directory (`cd`) first, so that the .log file produced by `wstata.exe` is put into the same directory as the .do file.  The `/c` parameter causes the `cmd.exe` shell to close when it's done.

### Stat-Transfer ###

Similar to writing and running Stata do files from Notepad++ (above), I have begun to do the same for [Stat-Transfer](http://www.stat-transfer.com)  Files.

  * I have posted a `userdefinelang.xml` file in the [repository](http://code.google.com/p/notepad-stats-integration/source/browse/).

  * To your shortcuts.xml file, add something similar to the following:

```
<Command name="Stat-Transfer command file" Ctrl="no" Alt="yes" Shift="no" Key="120">
	"C:\Program Files\StatTransfer9\st.exe" "$(FULL_CURRENT_PATH)"</Command> 
```

### Python ###

A Python script has been developed by Kyle H: `ipylines.au3`


> Hi Keith

> I've created a version of your program that allows passing of lines from Notepad++ to IPython (in this case PyLab from the Enthought Python Distribution). It's just some minor tweaks, but I thought you might find it interesting or want to add it to the google page (I'll put it on my own website eventually, but haven't had time yet).

> The changes are: (1) Restores clipboard after pasting into target program. (2) Creates a temporary .py file for multiple lines, but for single lines or just a portion of a line it copies and pastes the command directly (this is useful in Python so you can see the values returned, which running a .py file often suppresses). (3) Ditched the .ini for now, simply to make distribution easier among my colleagues.

> When I get a chance, I'm going to generalize it to have one key access to IPython, Stata, and R.

> Thanks so much for posting your code, saved me a lot of time!

> Best, Kyle

### LaTeX ###

LaTeX formatting is built-in to Notepad++.  If you've installed
[Miktex 2.7](http://miktex.org/) and Adobe Reader on windows, here's the Run command:

```
<Command name="PDFLaTex" Ctrl="yes" Alt="no" Shift="no" Key="190">cmd /c cd /d "$(CURRENT_DIRECTORY)" 
	&& pdflatex.exe -shell-escape "$(FILE_NAME)" && DEL "$(NAME_PART).log" && DEL file "$(NAME_PART).aux"</Command>
	
<Command name="PDFLaTex" Ctrl="yes" Alt="no" Shift="yes" Key="190">
	"C:\Program Files\Adobe\Reader 8.0\Reader\acrord32.exe" "$(CURRENT_DIRECTORY)\$(NAME_PART).pdf"</Command> 
```

### SAS ###

For SAS (in Windows) there’s a built-in command.  Thus, you just need one line to create another entry/keyboard shortcut in the “RUN” area of Notepad++.  There’s no need for AutoIt, at least for some people, some of the time.  The final command should be:

```
<Command name="SAS: Run entire file" Ctrl="yes" Alt="yes" Shift="yes" Key="120sas "$(FULL_CURRENT_PATH)"</Command>
```

If you can't run a SAS file from the "Run" box on your start menu, [see this page](http://support.sas.com/documentation/cdl/en/hostwin/61924/HTML/default/startsas.htm#a000104280).

To run the selected text, you can modify my rundolines.kak.au3 file.

I could easily see a program that would do something like this:
  1. Copy lines
  1. Paste these lines into a new temp file
  1. Submit the following command to Windows: ` sas "c:\myfolder\tempfile.sas" `


### Run anything from one key ###

I once received an email from Jelmer Ypma, who has [posted an AutoIt script](http://www.ucl.ac.uk/~uctpjyy/downloads.html) that can be used to run the file currently open in Notepad++ in a program of choice (based on the file extension).  You can quickly see how the .ini file works; it appears you could extend the idea to nearly any file extension.