
# Search


	Cherrytree’s search and replace features can be found in the **Search** menu.

 ## Steps to Perform a Search:Steps to Perform a Search:

	1. Select one of the following options from the **Search **menu:

			- **Find in Node Content** - Searches for a sequence of characters in the selected node’s content.

			- **Find in All Nodes Contents **- Searches for a sequence of characters in the entire node tree.

			- **Find in Selected Node and Subnodes Contents** - Searches for a sequence of characters in the selected node and its [children](https://docs.oracle.com/cd/E19509-01/820-3742/ghpow/index.html).

			- **Find in Nodes Names and Tags** - Searches for a sequence of characters in the node title and tag of the node tree.
	
				**NOTE:** See Tags for Searching in [Creating Nodes](../Nodes/Creating%20Nodes.md) for more detail.

			- **Find Again** - Find the next instance in the search results.

			- **Find Back** - Find the previous instance in the search results.
		
				**NOTE**: **Find Again** and** Find Back** are only compatible with the **First From Selection** and **First in All Range** options, which are defined in the next step.

	2. (**Optional**) Select any of the available [Search Options](Search.md).

	3. Enter the characters that you desire to find into **Search For** and click **OK** to execute the search.

 ## Steps to Search and ReplaceSteps to Search and Replace

	1. Select one of the following options from the** Search** menu:
	
		- **Replace in Node Content **- Searches for a sequence of characters in the selected node’s content and replaces them with the provided text.

		- **Replace in All Nodes Contents **- Searches for a sequence of characters in the entire node tree and replaces them with the provided text.

		- **Replace in Selected Node and Subnodes Contents** - Searches for a sequence of characters in the selected node and its [children](https://docs.oracle.com/cd/E19509-01/820-3742/ghpow/index.html), and replaces them with the provided text.

		-** Replace in Nodes Names and Tags** - Searches for a sequence of characters in every node title and tag of the node tree, and replaces them with the provided text.
		
			**NOTE: **See **Tags for Searching** in [Creating Nodes ](../Nodes/Creating%20Nodes.md)for more detail about node names and tags.

		- **Replace Again** - Find the next instance in the search results and replace it with the provided text.
		
			**NOTE: Replace Again** is only compatible with the **First From Selection** and **First in All Range** options, which are defined in the next step.

	2. (**Optional**) Select from the available [Search Options](Search.md).

	3. Enter characters to find into** Search For **and characters to replace in **Replace With**.

	4. Click **OK** to execute the search.


 ## Search OptionsSearch Options
	
	- **Match Case** - Filter results that do not match the [letter case](https://en.wikipedia.org/wiki/Letter_case) of the provided search term.

	- **Whole Word** - Filter results that contain more characters than provided. For example, a whole-word search for `and` returns any instances of the word** ****and** but not other words containing** ****and** such as **Andrew**.

	- **Regular Expression** - Search for patterns in text. For example, `\([0-9][0-9][0-9]\) [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]` would return instances of text formatted as (xxx) xxx-xxxx, such as phone numbers, where **x** can be any number between 0 and 9.
	
	** 	NOTE:** Learn more about regular expressions [here](https://developers.google.com/edu/python/regular-expressions).

	- **Start Word** - Filter results where the provided characters are not located at the beginning of the instance. For example, a start-word search for **cherry** would return **cherry** and **cherrytree** but not **treecherry**.

	- **Forward** - Search the node(s) from top to bottom. (Default)

	- **Backward **- Search the node(s) from bottom to top.

	- **All, List Matches** - Return all results. (Default)

	- **First From Selection** - Return only the first result closest to the cursor position.

	- **First in All Range** - Return only the first result of the node tree.

	- **Show Iterated Find/Replace Dialog **- Displays the **Iterate Latest Find/Replace**, which provides a graphical method of navigating through the search results.
	
		- **Close** - Closes the **Iterate Latest Find/Replace** menu.

		- **Find Previous **- Find the previous instance of the searched term.

		- **Find Next** - Find the next instance of the searched term.

		- **Replace **- Replace the current instance of the searched term with the replacement provided in Step 3 of[ Steps to Search and](Search.md)[ Replace](http://#_steps_to_search_and_replace). (Applicable only to Search and Replace features.)

		- **Undo** - Undoes the most recent Replace execution.

	- **Time Filter** options are available when searching across multiple nodes. Select any of the available option(s) and click the adjacent date(s) to edit its value:

	-** Node Created After** - Only show results from nodes created after the provided date.

	- **Node Created Before **- Only show results from nodes created before the provided date.

	- **Node Modified After** - Only show results from nodes that have been edited after the provided date.

	- **Node Modified Before** - Only show results from nodes that have been edited before the provided date.
