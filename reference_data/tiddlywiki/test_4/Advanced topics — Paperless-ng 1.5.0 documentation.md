https://paperless-ng.readthedocs.io/en/latest/advanced_usage.html#advanced-file-name-handling

# Advanced topics[](https://paperless-ng.readthedocs.io/en/latest/advanced_usage.html#advanced-file-name-handling#advanced-topics "Permalink to this headline")

Paperless offers a couple features that automate certain tasks and make your life
easier.

## Matching tags, correspondents and document types[](https://paperless-ng.readthedocs.io/en/latest/advanced_usage.html#advanced-file-name-handling#matching-tags-correspondents-and-document-types "Permalink to this headline")

Paperless will compare the matching algorithms defined by every tag and
correspondent already set in your database to see if they apply to the text in
a document. In other words, if you defined a tag called `Home`` ``Utility`
that had a `match` property of `bc`` ``hydro` and a `matching_algorithm` of
`literal`, Paperless will automatically tag your newly-consumed document with
your `Home`` ``Utility` tag so long as the text `bc`` ``hydro` appears in the body
of the document somewhere.

The matching logic is quite powerful, and supports searching the text of your
document with different algorithms, and as such, some experimentation may be
necessary to get things right.

In order to have a tag, correspondent or type assigned automatically to newly
consumed documents, assign a match and matching algorithm using the web
interface. These settings define when to assign correspondents, tags and types
to documents.

The following algorithms are available:

- **Any:** Looks for any occurrence of any word provided in match in the PDF.
  If you define the match as `Bank1`` ``Bank2`, it will match documents containing
  either of these terms.

- **All:** Requires that every word provided appears in the PDF, albeit not in the
  order provided.

- **Literal:** Matches only if the match appears exactly as provided in the PDF.

- **Regular expression:** Parses the match as a regular expression and tries to
  find a match within the document.

- **Fuzzy match:** I dont know. Look at the source.

- **Auto:** Tries to automatically match new documents. This does not require you
  to set a match. See the notes below.

When using the “any” or “all” matching algorithms, you can search for terms
that consist of multiple words by enclosing them in double quotes. For example,
defining a match text of `"Bank`` ``of`` ``America"`` ``BofA` using the “any” algorithm,
will match documents that contain either “Bank of America” or “BofA”, but will
not match documents containing “Bank of South America”.

Then just save your tag/correspondent and run another document through the
consumer. Once complete, you should see the newly-created document,
automatically tagged with the appropriate data.

### Automatic matching[](https://paperless-ng.readthedocs.io/en/latest/advanced_usage.html#advanced-file-name-handling#automatic-matching "Permalink to this headline")

Paperless-ng comes with a new matching algorithm called *Auto*. This matching
algorithm tries to assign tags, correspondents and document types to your
documents based on how you have assigned these on existing documents. It
uses a neural network under the hood.

If, for example, all your bank statements of your account 123 at the Bank of
America are tagged with the tag “bofa\_123” and the matching algorithm of this
tag is set to *Auto*, this neural network will examine your documents and
automatically learn when to assign this tag.

Paperless tries to hide much of the involved complexity with this approach.
However, there are a couple caveats you need to keep in mind when using this
feature:

- Changes to your documents are not immediately reflected by the matching
  algorithm. The neural network needs to be *trained* on your documents after
  changes. Paperless periodically (default: once each hour) checks for changes
  and does this automatically for you.

- The Auto matching algorithm only takes documents into account which are NOT
  placed in your inbox (i.e., have inbox tags assigned to them). This ensures
  that the neural network only learns from documents which you have correctly
  tagged before.

- The matching algorithm can only work if there is a correlation between the
  tag, correspondent or document type and the document itself. Your bank
  statements usually contain your bank account number and the name of the bank,
  so this works reasonably well, However, tags such as “TODO” cannot be
  automatically assigned.

- The matching algorithm needs a reasonable number of documents to identify when
  to assign tags, correspondents, and types. If one out of a thousand documents
  has the correspondent “Very obscure web shop I bought something five years
  ago”, it will probably not assign this correspondent automatically if you buy
  something from them again. The more documents, the better.

- Paperless also needs a reasonable amount of negative examples to decide when
  not to assign a certain tag, correspondent or type. This will usually be the
  case as you start filling up paperless with documents. Example: If all your
  documents are either from “Webshop” and “Bank”, paperless will assign one of
  these correspondents to ANY new document, if both are set to automatic matching.

## Hooking into the consumption process[](https://paperless-ng.readthedocs.io/en/latest/advanced_usage.html#advanced-file-name-handling#hooking-into-the-consumption-process "Permalink to this headline")

Sometimes you may want to do something arbitrary whenever a document is
consumed. Rather than try to predict what you may want to do, Paperless lets
you execute scripts of your own choosing just before or after a document is
consumed using a couple simple hooks.

Just write a script, put it somewhere that Paperless can read & execute, and
then put the path to that script in `paperless.conf` with the variable name
of either `PAPERLESS_PRE_CONSUME_SCRIPT` or
`PAPERLESS_POST_CONSUME_SCRIPT`.

Important

These scripts are executed in a **blocking** process, which means that if
a script takes a long time to run, it can significantly slow down your
document consumption flow. If you want things to run asynchronously,
you’ll have to fork the process in your script and exit.

### Pre-consumption script[](https://paperless-ng.readthedocs.io/en/latest/advanced_usage.html#advanced-file-name-handling#pre-consumption-script "Permalink to this headline")

Executed after the consumer sees a new document in the consumption folder, but
before any processing of the document is performed. This script receives exactly
one argument:

- Document file name

A simple but common example for this would be creating a simple script like
this:

`/usr/local/bin/ocr-pdf`

    #!/usr/bin/env bash
    pdf2pdfocr.py -i ${1}

`/etc/paperless.conf`

    ...
    PAPERLESS_PRE_CONSUME_SCRIPT="/usr/local/bin/ocr-pdf"
    ...

This will pass the path to the document about to be consumed to `/usr/local/bin/ocr-pdf`,
which will in turn call [pdf2pdfocr.py](https://github.com/LeoFCardoso/pdf2pdfocr) on your document, which will then
overwrite the file with an OCR’d version of the file and exit. At which point,
the consumption process will begin with the newly modified file.

### Post-consumption script[](https://paperless-ng.readthedocs.io/en/latest/advanced_usage.html#advanced-file-name-handling#post-consumption-script "Permalink to this headline")

Executed after the consumer has successfully processed a document and has moved it
into paperless. It receives the following arguments:

- Document id

- Generated file name

- Source path

- Thumbnail path

- Download URL

- Thumbnail URL

- Correspondent

- Tags

The script can be in any language you like, but for a simple shell script
example, you can take a look at `post-consumption-example.sh` in the
`scripts` directory in this project.

The post consumption script cannot cancel the consumption process.

## File name handling[](https://paperless-ng.readthedocs.io/en/latest/advanced_usage.html#advanced-file-name-handling#file-name-handling "Permalink to this headline")

By default, paperless stores your documents in the media directory and renames them
using the identifier which it has assigned to each document. You will end up getting
files like `0000123.pdf` in your media directory. This isn’t necessarily a bad
thing, because you normally don’t have to access these files manually. However, if
you wish to name your files differently, you can do that by adjusting the
`PAPERLESS_FILENAME_FORMAT` configuration option.

This variable allows you to configure the filename (folders are allowed) using
placeholders. For example, configuring this to

    PAPERLESS_FILENAME_FORMAT={created_year}/{correspondent}/{title}

will create a directory structure as follows:

    2019/
      My bank/
        Statement January.pdf
        Statement February.pdf
    2020/
      My bank/
        Statement January.pdf
        Letter.pdf
        Letter_01.pdf
      Shoe store/
        My new shoes.pdf

Danger

Do not manually move your files in the media folder. Paperless remembers the
last filename a document was stored as. If you do rename a file, paperless will
report your files as missing and won’t be able to find them.

Paperless provides the following placeholders withing filenames:

- `{asn}`: The archive serial number of the document, or “none”.

- `{correspondent}`: The name of the correspondent, or “none”.

- `{document_type}`: The name of the document type, or “none”.

- `{tag_list}`: A comma separated list of all tags assigned to the document.

- `{title}`: The title of the document.

- `{created}`: The full date and time the document was created.

- `{created_year}`: Year created only.

- `{created_month}`: Month created only (number 1-12).

- `{created_day}`: Day created only (number 1-31).

- `{added}`: The full date and time the document was added to paperless.

- `{added_year}`: Year added only.

- `{added_month}`: Month added only (number 1-12).

- `{added_day}`: Day added only (number 1-31).

Paperless will try to conserve the information from your database as much as possible.
However, some characters that you can use in document titles and correspondent names (such
as `:`` ``\`` ``/` and a couple more) are not allowed in filenames and will be replaced with dashes.

If paperless detects that two documents share the same filename, paperless will automatically
append `_01`, `_02`, etc to the filename. This happens if all the placeholders in a filename
evaluate to the same value.

Hint

Paperless checks the filename of a document whenever it is saved. Therefore,
you need to update the filenames of your documents and move them after altering
this setting by invoking the [document renamer](https://paperless-ng.readthedocs.io/en/latest/advanced_usage.html#advanced-file-name-handlingadministration.html#utilities-renamer).