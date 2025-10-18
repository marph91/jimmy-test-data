---
created: '2014-02-09T14:36:52.456000'
tags:
- tiddlywiki on node.js
title: MultiTiddlerFiles
updated: '2015-06-21T18:21:40.407000'
---

[MultiTiddlerFiles](./MultiTiddlerFiles.md) allow multiple tiddlers to be concisely represented in a single text file.

The goals of this format are:

* To be easy to type and easy to read
* Optimised for single line strings
* To allow common fields or tags to be shared within groups of tiddlers
* To be simple to process with external tools

[MultiTiddlerFiles](./MultiTiddlerFiles.md) have the extension `multids`. The file is structured as a block of shared fields followed by a blank line. The rest of the file is a sequence of comments and tiddlers. Tiddlers are specified by their title, followed by a colon, at least one space character, and then the rest of the line is the text field for the tiddler.

For example:

```
title: $:/language/ControlPanel/
tags: strings
modifier: JoeBloggs

Basics/Caption: Basics
1. This is a comment
Basics/Version: ~TiddlyWiki Version
```

This example defines two tiddlers, [$:/language/ControlPanel/Basics/Caption](broken-link $:/language/ControlPanel/Basics/Caption) and [$:/language/ControlPanel/Basics/Version](broken-link $:/language/ControlPanel/Basics/Version).

If a `title` field is specified in the header then it is treated as a prefix for the individual tiddlers defined in the title.

## Syntax Specification

{{MultiTiddlerFileSyntax}}