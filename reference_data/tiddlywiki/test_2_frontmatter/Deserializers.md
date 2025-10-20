---
created: '2023-06-27T09:36:50.105000'
tags:
- features
title: Deserializers
updated: '2023-06-27T09:43:56.394000'
---

[Features](broken-link Features)

Deserializer [modules](./Modules.md) parse text in various formats into their JSON representation as tiddlers. The deserializer modules available in a wiki can be seen using the  [deserializers operator](<./deserializers Operator.md>) and can be used with the [deserialize Operator](<./deserialize Operator.md>).

The TiddlyWiki core provides the following deserializers:

| Deserializer | Description |
| --- | --- |
| (DOM) | Extracts tiddlers from a DOM node, should not be used with the <<.op deserialize[]>> operator |
| application/javascript | Parses a [JavaScript](./JavaScript.md) module as a tiddler extracting fields from the header comment |
| application/json | Parses [JSON](<./JSON in TiddlyWiki.md>) into tiddlers |
| application/x-tiddler | Parses the [.tid file format](./TiddlerFiles.md) as a tiddler |
| application/x-tiddler-html-div | Parses the [<DIV>.tiddler file format](tiddlywiki://TiddlerFiles) as a tiddler |
| application/x-tiddlers | Parses the [MultiTiddlerFile format](./MultiTiddlerFiles.md) as tiddlers |
| text/css | Parses CSS as a tiddler extracting fields from the header comment |
| text/html | Parses an HTML file into tiddlers. Supports ~TiddlyWiki Classic HTML files, ~TiddlyWiki5 HTML files and ordinary HTML files |
|text/plain|Parses plain text as a tiddler|