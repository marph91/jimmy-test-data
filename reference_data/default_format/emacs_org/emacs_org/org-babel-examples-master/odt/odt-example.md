\<2015-02-14 Sat\>

#  Version information

    Emacs version: GNU Emacs 24.4.1 (x86_64-unknown-linux-gnu, GTK+ Version 3.10.8)
     of 2014-10-31 on dflt1w

org version: 8.2.10

#  Table example

The table occupies 80% of the page width. The columns widhts will
be in the ratio of 4:7:10:10. Col b and col c have no visible
vertical separating line (they are one **column group**).

| col a |     |     |     |
|-------|-----|-----|-----|

Here we use a table reference: The compute resources of the
Swiss-CMS TIER-3 are shown in Table .

Note that the numbering of tables and figures is done in a format of section-number.sequence-number.
This cannot be configured by styles. I traced it to the source code in ox-odt.el

Table 2.1: PSI CMS Tier-3 Resources

| **Resources Q2/2013** |     |
|-----------------------|-----|

#  Page breaks and tinkering with OpenDocument XML

At first I wanted to use soft-page-break elements, as I saw them
in some LibreOffice generated files. But I found out that they only
work if in the enclosing \<office:body\> there is some definition
like this:

\<office:text text:use-soft-page-breaks="true"\>

Therefore the following inline ODT block does not work with the
default documents produced by the org ODT exporter, where that
setting is missing (at least not in LibreOffice). I confirmed that
the inline block had been included in the exported ODT document

    #+BEGIN_ODT
      <text:soft-page-break/>

#+END\_ODT

The basics of this are described in the [OASIS](http://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part1.html#__RefHeading__1419322_253892949) standards specification.

A method that works is to define our own style element for a page
break, just as it is described in the org ODT manual. I used the
styles.odt files that I had produced previously, unpacked it, and
then edited the styles.xml file found in the archive. Afterwards
I packed it again into an archive styles-df.odt and defined the
=#+ODT~STYLESFILE~: "./styles-df.odt"= setting for every org file
where I want to use it. And it works!

    </office:styles>
     ...
     <style:style style:name="PageBreak" style:family="paragraph"
                  style:parent-style-name="Text_20_body">
       <style:paragraph-properties fo:break-before="page"/>
     </style:style>

\</office:styles\>

Now, will we get a page break following this line?

#  Figure

The resource usage of the Swiss CMS Tier-3 since 2009 is shown in figure .

Figure 4.1: T3 resource usage