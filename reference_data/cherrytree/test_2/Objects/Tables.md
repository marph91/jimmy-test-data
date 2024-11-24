
# Tables


 ## Creating a New Table

	1. Select **Insert Table** from the** Edit** menu to display the** Insert Table **menu.

	2. The **Insert Table **menu defines the size of the table and provides** .csv** import availability.
	
		- **Rows** - Defines the number of rows to be in the table in the addition to the header row.

		- **Columns** - Defines the number of columns to be in the table.

		-** Min Width** - Defines the lowest number of pixels in width that a column must have.

		- **Max Width** - Defines the highest number of pixels in width that a column can have.

		- **Import from CSV File** - Imports data from a **.csv** file. Data should be separated by a comma delimiter.
		
			**NOTE:** Cherrytree may take a few minutes to upload a large file.

	3. Click **OK **to complete the insertion.


 ## Managing Columns

	Click a column title to display a menu listing actions for that column.

		- **Rename Column** - Changes the title of the selected column.

		- **Delete Column **- Deletes the selected column.

		- **Add Column **- Adds a new column to the right of the selected column.

		- **Move Column Left** - Switches the placement of the selected column with that of the column to its immediate left. Nothing happens if there is no column left of the selected column.

		- **Move Column Right **- Switches the placement of the selected column with that of the column to its immediate right.  Nothing happens if there is no column right of the selected column.

  ## Managing Rows

	Right-clicking any cell in a table provides the following options:

	- **Cut Table **- Moves the selected table to your clipboard. The table can then be pasted elsewhere.

	- **Copy Table** - Copies the selected table to your clipboard. A copy of the table can then be pasted elsewhere.

	- **Delete Table** - Deletes the selected table.

	- **Add Row** - Adds a new row underneath the selected row.

	- **Cut Row **- Moves the selected row to your clipboard. The row can then be pasted elsewhere.

	- **Copy Row** - Copies the selected row to your clipboard. A copy of the row can then be pasted elsewhere.

	- **Paste Row** - Pastes a row from your clipboard underneath the selected row.

	- **Delete Row** - Deletes the selected row.

	- **Move Row Up **- Switches the placement of the selected row with that of the row immediately above it. Nothing happens if there is no row above the selected row.

	- **Move Row Down **- Switches the placement of the selected row with that of the row immediately below it. Nothing happens if there is no row below the selected row.

	- **Sort Rows Descending** - References the first column to sort the selected table numerically then alphabetically, from bottom to top.

	- **Sort Rows Ascending **- References the first column to sort the selected table numerically then alphabetically, from top to bottom.

	- **Edit Table Properties** -  Displays the **Edit Table** **Properties** menu, providing options to define a minimum and maximum width of columns.
	
		- **Min Width **- Columns are always at least `x` pixels wide, where `x` represents the number provided.

		- **Max Width **- Columns cannot be wider than `x` pixels in width, where `x` represents the number provided. If the content exceeds the maximum width, text wraps to the next line within the cell.

	- **Table Export** - Exports the selected table to a .**csv** file containing data separated by comma delimiters.

 ## Writing to Tables

	Tables currently only support [plain text](../Text/Plain%20Text.md). Double-click a cell to open a textbox within it.

	**CAUTION**: Clicking outside of a table before closing a textbox discards all changes to that textbox. To write changes to a textbox within a table cell, you must click to another cell, press Enter,  or press Tab. This has been reported but is unlikely to be patched in this version of Cherrytree.

	Right-click the textbox to display a menu of its actions and properties.

	- **Cut **- Moves the selected text to your clipboard. The row can then be pasted elsewhere.

	-** Copy **- Copies the selected text to your clipboard. A copy of the table can then be pasted elsewhere.

	-** Paste** - Pastes the text from your clipboard to the cursor position.

	- **Delete **- Deletes the selected text.

	- **Select All **- Selects the text within the textbox.

	- **Input Methods **- Select from one of the following input methods:
	
		- System (Default)

		- None

		- Amharic (EZ+)

		- Cedilla

		- Cyrillic (Transliterated)

		- Inuktitut (Transliterated)

		- IPA

		- Multipress

		- Thai-Lao

		- Tigrigna-Eritrean (EZ+)

		- Tigrigna-Ethiopian (EZ+)

		- Vietnamese (VIQR)

		- Windows IME

	-** Insert Unicode Control Character** - Select from one of the following Unicode control characters:

		- **LRM **- Left-to-right mark

		- **RLM **- Right-to-left mark

		- **LRE  **- Left-to-right embedding

		- **RLE  **- Right-to-left embedding

		-** LRO**  - Left-to-right override

		- **RLO**  - Right-to-left override

		- **PDF**  - Pop directional formatting

		- **ZWS** - Zero width space

		- **XWJ**  - Zero width joiner

		- **XWNJ **- Zero width non-joiner
		
	- **Insert NewLine** - Adds a newline character to the current cursor position.

	**NOTE:** Newlines within table cells are not noticeable until the textbox is closed.
