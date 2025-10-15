---
created: '2013-08-26T12:20:00'
tags:
- mechanisms
title: PluginMechanism
updated: '2024-05-20T16:28:28.577000'
---

# Introduction

[Plugins](./Plugins.md) are bundles of tiddlers that are distributed and managed as a single unit. Users can install them with drag and drop, or using the [plugin library](broken-link Installing a plugin from the plugin library).

<<.from-version "5.1.22">> Plugins that contain JavaScript modules require a reload of the wiki before they will work. Plugins that do not contain JavaScript modules are automatically dynamically loaded and unloaded. 

Plugins can be used to package any tiddler content, including JavaScript [modules](./Modules.md) that extend and enhance the core TiddlyWiki5 functionality. The tiddlers within registered plugins are ShadowTiddlers: they can be freely overwritten by creating a tiddler with the same title, but deleting that tiddler restores the underlying tiddler value from the plugin.

By convention, plugin titles have the form `$:/plugins/<publisher>/<name>`. Plugins that are part of the core TiddlyWiki distribution have titles of the form `$:/plugins/tiddlywiki/<name>`.

When [running TiddlyWiki under Node.js](broken-link TiddlyWiki on Node.js), plugins can also be stored as individual tiddler files in [PluginFolders](broken-link PluginFolders).

# Plugin Stability

{{Plugin Stability}}

# Plugin Types

{{Plugin Types}}

# Plugin Dependencies

{{Plugin Dependencies}}

# Plugin Ordering

{{Plugin Ordering}}

# Plugin Fields

{{Plugin Fields}}

# More information

<<list-links "[PluginMechanism](tiddlywiki://PluginMechanism)">>