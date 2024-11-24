
# Saving


 ## Saving to the Current File

	Save your document by pressing **`CTRL`**+**`S`** or by selecting** Save **from the **File **menu.
	
	**NOTE:** If this your first time saving the current document, see the [save to a new file ](Saving.md)section below.

 ## Saving to a New File

	1. Save your document to a new file by pressing **`CTRL`**+**`SHIFT`**+**`S`** or by selecting **Save As** from the **File** menu.

	2. Select a [storage type](http://#_storage_types).

	3. Name the document and select a folder to save it to.

 ## Save and Vacuum

	Vacuuming rebuilds the database file, packing it into a minimal amount of disk space. Empty space is left behind when a large amount of data is deleted from a database. Frequent inserts, updates, and deletes can also cause the database file to become fragmented — where data for a single table or index is scattered around the database file.

	This feature should be used periodically when working with SQLite files to keep the database from assuming more space than necessary.

	**NOTE:** Visit the [SQLite documentation page for the vacuum command](https://www.sqlite.org/lang_vacuum.html) to learn more about vacuuming.

 ## Storage Types

	When saving a document for the first time, Cherrytree prompts you to choose between two file formats, SQLite and XML.

	**SQLite** is a self-contained database and has a **.ctb **or .**ctx** extension when used with Cherrytree. Instead of loading the complete document at runtime, Cherrytree only accesses the tree structure and selected node. This makes opening your document faster but may slow functions such as searching and selecting nodes when they’re used for the first time in a session. Only modified nodes are rewritten upon saving, decreasing save time.

	Performance loss with SQLite is lower than with XML, making it better suited for larger documents. The [Save and Vacuum](Saving.md) feature should be used periodically to keep SQLite files compact.

	**XML** is a markup language and has a **.ctd **or  **.ctz** extension when used with Cherrytree. These files are fully loaded at runtime, making searching and navigating through nodes faster, but slowing the initial load time. They are also completely rewritten upon saving, slowing the save process.

	XML is more accessible and easier to convert to other file types but should not be used with large documents.

 ## Password Protection

	Password-protected files are compressed and locked with [7zip](https://www.7-zip.org/), an open source file archiver.
		
	**NOTE:** Other applications might not provide functionality to unlock files that have been locked by Cherrytree.

 ## Changing Passwords

	To change the password of a protected file:
	
		1. Open the file in Cherrytree.

		2. Select Save-as from the File menu.

		3. [Save the document as a new file](Saving.md).
	
			1. Select a protected storage type.

			2. Use a new password to protect this copy of the document.


