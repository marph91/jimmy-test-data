
# Codebox


	A codebox is a contained, executable section of syntax-highlighted text, which can be inserted into [Rich Text](<../Text/Rich Text.md>) nodes. A Rich Text node can contain more than one codebox for any of the [supported languages](<../Text/Automatic Syntax Highlighting.md>).

	See [Automatic Syntax Highlighting](<../Text/Automatic Syntax Highlighting.md>) for more details about syntax highlighting.

 ## Inserting a Codebox

	1. Select **Insert Codebox** from the **Edit** menu.

	2. (**Optional**) Change the codebox type within the Insert Codebox menu:
	
		- **Plain Text** - Restricts the codebox to [plain text](<../Text/Plain Text.md>).

		- **Automatic Syntax Highlighting** - Applies [automatic syntax highlighting](<../Text/Automatic Syntax Highlighting.md>) to the codebox. (Default)

		- **Choose a language** - Select from any of the [supported languages](<../Text/Automatic Syntax Highlighting.md>).

	3. (**Optional**) - Define the codebox size:
	
		- **Width** - Defines the width of the codebox.
	
		- **Pixels** - Defines the width in pixels. (Default)

		- **% (Percentage)** -  Defines the width as a percentage. This assigns a dynamic width that changes alongside changes in the window’s width.

		- **Height** - Defines the height of the codebox in pixels.

	4. (**Optional**) Select any additional options:
	
		- **Show Line Numbers** - Display line numbers within the left margin of the codebox.

		- **Highlight Matching Brackets** - Highlights the corresponding bracket of the selected opening or closing bracket.

	5. Click **OK** to complete the insertion.

 ## Editing a Codebox

	Right-click a codebox to display its options.
	
	- **Change CodeBox Properties** - Displays a menu similar to the Insert CodeBox menu.

	- **Execute CodeBox Code** - Executes the code within the codebox.

		**NOTE:** See Executing a Codebox for more details.

	- **CodeBox Load From Text File** - Imports code from a file. This function is not restricted to files that have a .txt extension.

	- **CodeBox Save To Text File** - Exports the content of a codebox to a file. The file can have any extension.

	- **Cut CodeBox** - Moves the selected codebox to your clipboard. The codebox can then be pasted elsewhere.

	- **Copy CodeBox** - Copies the selected codebox to your clipboard. A copy of the codebox can then be pasted elsewhere.

	- **Delete CodeBox** - Delete the selected codebox.

	- **Delete CodeBox Keep Content** - Replace the current codebox with a [plain text](<../Text/Plain Text.md>) copy of its content.

	- **Increase CodeBox Width** - Increase the width of the selected codebox by 9% if it is defined as a percentage or 15px if it is defined in pixels.

	- **Decrease CodeBox Width** - Decrease the width of the selected codebox by 9% if it is defined as a percentage or 15px if it is defined in pixels.

	- **Increase CodeBox Height** - Increase the height of the selected codebox by 15 pixels.

	- **Decrease CodeBox Height** - Decrease the height of the selected codebox by 15 pixels.

 ## Executing a Codebox

	A codebox that is set to [automatic syntax highlighting](<../Text/Automatic Syntax Highlighting.md>) can be executed from Cherrytree, assuming you have its assigned language installed to your machine.

	**To execute a node:**

		1. Right-click a codebox and select **Execute Codebox** code.

		2. When prompted, click **OK** to confirm that you want to execute the code.

	Some languages require an execution command to be assigned to the language before the code can be executed.
	
	See [Plain Text and Code](<../Settings/Plain Text and Code.md>) for details on assigning a command.
