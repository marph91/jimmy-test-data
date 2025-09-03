This zim wiki sample notebook was created for the [https://github.com/gsantner/markor](https://github.com/gsantner/markor) project by [Gregor Santner](https://github.com/gsantner) and is licensed under [Creative Commons Zero 1.0](https://creativecommons.org/publicdomain/zero/1.0/legalcode) (public domain). File revision 1.

## Zim Notebook Structure

In the same directory as this page, there is a text file named "notebook.zim". It specifies that this is the root of the notebook.
The text file for each page has a ".txt" file ending. The file name corresponds to the page title, but space characters (" ") are represented as underlines ("_").
All files and pages which are children of this page are located in a folder named according to the page file.

Example: This page is stored as a text file with the name "Root_Page.txt" in the root of the notebook. Subpages and files relative to this page are located in a folder named "Root_Page", which is also in the root of the notebook.

## Headings (this is H2)

### Heading Level 3

#### Heading Level 4

##### Heading Level 5

## Basic Syntax Elements

**Bold**
*italics*
==marked (yellow Background)==
~~striked~~

You can combine those styles:
***this is italic and bold***
***This is italic and bold (and Zim will automatically swap the stars with the slashes if you edit it)***
**==This is marked yellow and bold==**

This is `preformatted text` inline.

```
This is a preformatted text block.
It spans multiple lines.
And it's visually indented.
```

We also have ~subscript~ and ^superscript^.

## Lists

### Unordered Lists

* Unordered List
* second item
    * Sub-Item
        * Subsub-Item
            * and one more sub
* Back to first indent level

### Ordered Lists

1. ordered list
2. second item
    a. item 2a
        1. Item 2a1
        2. Item 2a2
    b. item 2b
        1. 2b1
            a. 2b1a
3. an so on...

### Checklists

- [ ] Checklist
- [ ] unchecked item
- [x] checked item
- [x] crossed item
- [ ] Item marked with a yellow left-to-right-arrow
- [ ] another unchecked item

## Links

This is an embedded web link: [Markor on Github](https://github.com/gsantner/markor)

To link relatively **down** the hierarchy to a sub page from the current page, use a "+" in front of the path to the page:
[Sub-page link to Sub Page 1](<./Root_Page/Sub Page 1.md>)
[Sub-page link to Sub Sub Page 1-1](<./Root_Page/Sub_Page_1/Sub Sub Page 1-1.md>)

To link absolutely to any page in the notebook, use ":", followed by the notebook root page:
[Absolute link to Sub Page 1](<./Root_Page/Sub Page 1.md>)

For relative links that go **up** in the hierarchy, see the information [on this page](<./Root_Page/Sub_Page_1/Sub Sub Page 1-1.md>).

If you don't need a different text displayed for the underlying link and just want the link to be visible, there is no need for the "|" delimiter. Just use double square brackets around the link:
[Sub Page 1](<./Root_Page/Sub Page 1.md>)

Directly inserted URLs will be displayed as links automatically and don't need any brackets:
https://github.com/gsantner/markor

## Images

The following image belongs to the current page and is located in the folder for "Root Page":
![flowerfield.jpg](./flowerfield.jpg)
