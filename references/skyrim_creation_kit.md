## Skyrim Creation Kit Information

### Questions

1. Is it better to use the creation kit from the Bethesda Launcher or the Steam Library Toolkit?


### Creation Engine Data Format

1. Master Files - .esm files; large collections of data.
2. Plugins - .esp files; small collections of data loaded on top of Master Files. May modify or reference data in a master file, or add new data.

In the game, multiple Plugins may be loaded. 

In the Creation Kit, only one plugin may be considered the 'active file', meaning any changes will be saved to that plugin when the user saves.


### First Plugin

1. Use the skyrim.esm and Update.esm files as your plugin's master files. Load them with the menu: File>Data. Ignore any warnings, they are supposed to happen... 
2. Create your plugin in the menu: File>Save. Since you have no active plugin, you will be prompted to create a new .esp file. NOTE: There is no "save as" feature. All saves will overwrite the current plugin. Versioning must be done outside the program. Your saved plugins are found directly in your Skyrim\Data\ folder.
3. Load Plugins in Special Edition: In the main game menu choose Mods>Load Order and activate your local plugins.

```
Demo Console Commands:
`TGM` - Toggle God Mode
`TWF` - ToggleWireframe
`COC RiverwoodSleepingGiantInn` - teleport to Riverwood inn

Save games made with mods or console commands might be broken!! Make sure any saves you care about are backed up before testing and don't save over them.
```

### Papyrus Scripting Info for Experienced Programmers

- [Papyrus Primer](http://www.creationkit.com/index.php?title=Papyrus_Introduction)
- [Papyrus Events & Properties (goog cache)] (https://webcache.googleusercontent.com/search?q=cache:eXVPDMVDaTsJ:https://www.creationkit.com/index.php%3Ftitle%3DBethesda_Tutorial_Papyrus_Events_and_Properties+&cd=1&hl=en&ct=clnk&gl=us)
- [Level Design Series](http://www.creationkit.com/index.php?title=Category:Bethesda_Level_Design_Tutorial_Series)


#### Papyrus Programming References

- [Literals Reference](https://www.creationkit.com/index.php?title=Literals_Reference)
- [Operator Reference](https://www.creationkit.com/index.php?title=Operator_Reference)
- [Statement Reference](https://www.creationkit.com/index.php?title=Statement_Reference)
- [Variable Reference (cache)](https://webcache.googleusercontent.com/search?q=cache:9KXbJ3Cj_tgJ:https://www.creationkit.com/index.php%3Ftitle%3DVariable_Reference+&cd=1&hl=en&ct=clnk&gl=us)
- [Variables and Properties](http://www.creationkit.com/index.php?title=Variables_and_Properties)


### Creation Kit Wiki References

- [Creation Kit Wiki Main Page](http://www.creationkit.com/index.php?title=Main_Page)
 
- [Getting Started (creation kit tour)](http://www.creationkit.com/index.php?title=Category:Getting_Started)
 
- [Creation Kit Wiki Content Statistics](http://www.creationkit.com/index.php?title=Special:MediaStatistics)
 
- [Papyrus "Hello World" Script](http://www.creationkit.com/index.php?title=Bethesda_Tutorial_Papyrus_Hello_World)
    - I did this and it worked. Simple intro to check that your toolchain works.


### Creation Kit Wiki Categories

- [Category:Tutorials](http://www.creationkit.com/index.php?title=Category:Tutorials)
 
- [Category:Game_Systems](http://www.creationkit.com/index.php?title=Category:Game_Systems)
 
- [Category:Editor_Reference](http://www.creationkit.com/index.php?title=Category:Editor_Reference)
 
- [Category:Getting_Started](http://www.creationkit.com/index.php?title=Category:Getting_Started)
 
- [Category:Keyboard_Mapping](http://www.creationkit.com/index.php?title=Category:Keyboard_Mappings)
 
- [Category:Papyrus](http://www.creationkit.com/index.php?title=Category:Papyrus)
 
- [Category:Designer_Debug_Tools](http://www.creationkit.com/index.php?title=Category:Designer_Debug_Tools)



### Additional Resources

- [Skyrim Special Edition Creation Kit Fine-Tuning](http://www.nexusmods.com/skyrimspecialedition/news/12935/?)
- [Converting Standard mods to SE](http://afkmods.iguanadons.net/index.php?/topic/4633-skyrim-se-things-to-know-when-converting-standard-mods-to-sse/)

#### Community Resources

- https://www.reddit.com/r/skyrimmods/wiki/guides_and_resources
- http://forums.bethsoft.com/forum/117-v-skyrim-skyrim-special-edition/
- http://forums.bethsoft.com/forum/184-the-creation-kit/