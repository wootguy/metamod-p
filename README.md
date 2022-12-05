This readme goes over the basics for installing Metamod and managing Metamod plugins for Sven Co-op. For more advanced usage and configuration, see [this page](http://metamod.org/metamod.html).

# Installing Metamod

1. Download https://github.com/wootguy/metamod-p/releases/tag/1.12p38_fix
2. Create folders `svencoop/addons/metamod/dlls`
3. Extract `metamod.dll` (Windows) or `metamod.so` (Linux) into `svencoop/addons/metamod/dlls/`
4. Create empty file `svencoop/addons/metamod/plugins.ini`
5. Add one of these launch options to the game, depending on your OS:
    - Windows: `-dll addons/metamod/dlls/metamod.dll`
    - Linux: `-dll addons/metamod/dlls/metamod.so` 
6. Start the game and test that Metamod works by typing `meta version` in the console.

# Installing Metamod Plugins
Each plugin may have its own special installation steps, but all plugins should share the steps below.

1. Download the plugin files. You should at least have a .dll and .so file.
1. Add the plugin file to your dlls folder:
    - For Windows, extract the .dll file to `svencoop/addons/metamod/dlls/`
    - For Linux, extract the .so file to `svencoop/addons/metamod/dlls/`
1. Add the .dll or .so path to your plugins.ini file. You need to add `win32` or `linux` before the path, depending on your OS (see examples below).
1. Type `meta refresh` in your server console to load the new plugins, or restart the server.

plugins.ini is where you list the plugins you want to load. It's similar to the default_plugins.txt file for angelscript, but much simpler.

Here's an example plugins.ini for Windows with a couple of plugins installed:
```
win32 addons/metamod/dlls/example_plugin.dll
win32 addons/metamod/dlls/another_plugin.dll
```

and the same example but for a Linux system:
```
linux addons/metamod/dlls/example_plugin.so
linux addons/metamod/dlls/another_plugin.so
```

You can start a line with the `#` character to write comments or disable plugins. Here's an example plugins.ini with comments and the "another_plugin" plugin disabled:
```
# Hello welcome to my plugins.ini
# This is where I write my plugin paths

win32 addons/metamod/dlls/example_plugin.dll
#win32 addons/metamod/dlls/another_plugin.dll
# ^ hmm something is wrong with this plugin. I disabled it for now.
```

**WARNING:** Disabling/unloading plugins on a live server may cause a crash.

# Updating plugins on a live server
When installing a new plugin, all you need to do is type `meta refresh` in the server console to load it. If you want to update a plugin without restarting the server, you'll need follow the steps below.

### Windows
1. Rename the old plugin .dll to something else ("Example.dll" -> "Example_lolololol.dll")
1. Copy the new .dll file to the same place, using the old name ("Example.dll")
1. Type `meta list` in console to find the name of the plugin that needs reloading.
1. Type `meta reload Example` in console to reload the plugin (replacing "Example" with the name of the plugin found in the previous step).

In my experience, using `meta refresh` or `meta unload` to reload plugins will crash the game.

### Linux
1. Type `meta list` in console to find the name of the plugin that needs reloading.
1. Type `meta unload Example` to unload the current version of the plugin (replacing "Example" with the name of the plugin found in the previous step).
    - **WARNING:** Some plugins will crash the server at this step. In those cases you just always need to restart the server to update.
1. Replace the plugin .so file with the updated version.
1. Type `meta refresh` to reload the plugin.
