# Introduction

Plugins in TiddlyWiki5 can be used to distribute optional components that customise and extend wiki. You can install them from the official plugin library or from community sites.

Internally, plugins are a bundle of tiddlers packaged together as a single tiddler that can be installed, copied, disabled or deleted as a unit. The individual tiddlers within a plugin appear as shadow tiddlers. 

Plugins can contain ~JavaScript modules, style sheets, and templates. Plugins can also be used to distribute ordinary text, images or any other content.

# Handling Plugins with a Single File Wiki

<<list-links "">>

# Handling Plugins with a Client - Server Configuration (Node.js)

<<list-links "">>

# Plugin Mechanism

The PluginMechanism tiddler contains more details about how plugins are implemented internally. 

You can open the plugin details in the <<controlPanel-plugin-link>> on the <<.controlpanel-tab Plugins>> sub-tab.

There is a plugin called $:/core that contains the main core code of TiddlyWiki. It is always present, and it is the source of default ShadowTiddlers.