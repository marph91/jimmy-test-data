---
created: '2014-09-10T21:55:14.237000'
tags:
- concepts
- tableofcontents
title: Plugins
updated: '2022-06-17T13:38:19.755000'
---

[Concepts](./Concepts.md), [TableOfContents](broken-link TableOfContents)

# Introduction

Plugins in TiddlyWiki5 can be used to distribute optional components that customise and extend wiki. You can install them from the official plugin library or from community sites.

Internally, plugins are a bundle of tiddlers packaged together as a single tiddler that can be installed, copied, disabled or deleted as a unit. The individual tiddlers within a plugin appear as shadow tiddlers. 

Plugins can contain ~JavaScript modules, style sheets, and templates. Plugins can also be used to distribute ordinary text, images or any other content.

# Handling Plugins with a Single File Wiki

<<list-links "[Plugins](tiddlywiki://Plugins) -[draft.of](tiddlywiki://draft.of)">>

# Handling Plugins with a Client - Server Configuration (Node.js)

<<list-links "[PluginsCS](tiddlywiki://PluginsCS) -[draft.of](tiddlywiki://draft.of)">>

# Plugin Mechanism

The [PluginMechanism](./PluginMechanism.md) tiddler contains more details about how plugins are implemented internally. 

You can open the plugin details in the <<controlPanel-plugin-link>> on the <<.controlpanel-tab Plugins>> sub-tab.

There is a plugin called $:/core that contains the main core code of TiddlyWiki. It is always present, and it is the source of default ShadowTiddlers.