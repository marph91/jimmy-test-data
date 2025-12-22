---
created: '2025-12-20T05:11:13.002000'
tags:
- book
- company
- person
title: The power of Backlinks
updated: '2025-12-20T05:11:15.621000'
---

# The power of Backlinks

In Reflect there are two ways of organizing your notes: backlinks and tags.

- Backlinks are a way of *linking notes* to each other, associating the two.

- Tags are a way of *categorizing notes*.

Let's dive into each.

## **Using Backlinks**

A backlink is just a link between two notes. You should be back-linking any entities you reference in your notes. (For example, an entity might be a particular person, company, or location.)

Generally you'll be working in today's daily note, and creating back-links from there. In this example we're going to backlink *Ankit Pansari*, a person we just met with.

![backlinking](https://firebasestorage.googleapis.com/v0/b/reflect-prod.appspot.com/o/users%2FgjzQZB390LOY9DmlguxzrU6xaHw2%2F16f80aa26aaa4af39813e354a8ae65cf?alt=media&token=3718e2c8-bae0-4f9a-8d86-c1043a469f68)

Let's try it. To create a backlink, type `[[` and then the entity name.

You'll then either select an existing note (use the arrow keys) or create a new blank note. Hit `enter` or `tab` to create the backlink.

Backlinks are case-sensitive and should be the full entity name (use New York City rather than NYC).

### Incoming backlinks

Clicking on the purple backlink will show you the linked note. In this example, notice that the *incoming backlinks* panel at the bottom of the note titled *Ankit Pansari* has a reference back to the daily note linking to it.

![backlinks](https://firebasestorage.googleapis.com/v0/b/reflect-prod.appspot.com/o/users%2FgjzQZB390LOY9DmlguxzrU6xaHw2%2Fd0139d51dc1642be84cdcbd77a200273?alt=media&token=80a1672d-2432-4b4c-ab96-f907c613193e)

You can start to see how this would start to build up an activity feed of your meetings with *Ankit*.

### Forming a graph

Over time these back-linked associations form a graph, in a similar fashion to the way neurons work in your brain.

You can see this graph forming under the *Map* tab. Here's mine:

![graph view](https://firebasestorage.googleapis.com/v0/b/reflect-prod.appspot.com/o/users%2FgjzQZB390LOY9DmlguxzrU6xaHw2%2F9cdf86dc78944abc8e71e5840acbd8b7?alt=media&token=c90d1160-f69f-4db1-9eeb-280365aed889)

So what’s the point of all this backlinking (other than creating pretty visualizations)? The answer is to do with recall.

Let’s just say you backlink Ankit to the company he works for, OSlash.

![linking oslash](https://firebasestorage.googleapis.com/v0/b/reflect-prod.appspot.com/o/users%2FgjzQZB390LOY9DmlguxzrU6xaHw2%2F18373ea4a927498e871b44df4889094f?alt=media&token=22c60e5d-d32a-4b91-9e9c-99be5b74e9fa)

Now you can pull up the company note quickly (`cmd k`). And then see anyone working at that company.

![command k](https://firebasestorage.googleapis.com/v0/b/reflect-prod.appspot.com/o/users%2FgjzQZB390LOY9DmlguxzrU6xaHw2%2F094f2c33d64d4e0ea46e3ad42cdadc40?alt=media&token=d18389f0-22a8-497b-953b-74def1ef62eb)

You can also go in the opposite direction, pulling up employees and seeing where they work.

You can extend this to all sorts of things, like backlinking specific locations, or projects that you’re working on.

When you forget something, say a name, type what you do remember into Reflect. And you’ll be able to follow the associations to whatever you’ve forgotten.

## **Categorizing with tags**

So now we've seen how backlinks work, let's move onto tags. In this example *OSlash* is Ankit's company. Let's navigate to that company's dedicated note and decorate it with the company website and `#company` hashtag.

Tags can be created by typing the hash symbol (`#`) and then the tag-name. Our convention for tag names is lowercase singular without spaces. Hit enter or tab to insert the tag.

![create tag](https://firebasestorage.googleapis.com/v0/b/reflect-prod.appspot.com/o/users%2FgjzQZB390LOY9DmlguxzrU6xaHw2%2F29225073939e4a2486a6efb9c89d45c5?alt=media&token=6d0fa6c3-a364-463a-8836-0697af28e6e8)

We pre-create some system level tags (like `#person`), but in the example above we're creating a custom `#company` tag.

### Listing notes by tag

Now that the note has a custom `#company` hashtag we can navigate to it easily under *All notes*.

While some system tags are elevated (people/books/etc), custom tags are available under the far right context menu.

![custom tag](https://firebasestorage.googleapis.com/v0/b/reflect-prod.appspot.com/o/users%2FgjzQZB390LOY9DmlguxzrU6xaHw2%2Ff447bdd11a154a0abb1afa2c7269ed43?alt=media&token=07ea48d1-70cb-4a9c-a439-8f5807755093)

## **Backlinks vs Tags**

We often get asked, when do I use a backlink and when do I use a tag? The answer is simple:

- For entities use backlinks

- For categories use tags

If something doesn't fit neatly into one of these buckets, default to using a backlink.

### Examples of backlinks and tags:

For example, these entities would be backlinks: Alex MacCaw, Google, New York.

And these categories would be tags: #book, #company, #person

Notice we use the convention of singular lower-case for tags.

### Why this distinction?

The reason lies behind the different behavior when clicking on a backlink vs a tag.

Clicking on a *backlink* takes you to a dedicated note, which is what you'd want to see for an entity (like a particular person).

Every time that dedicated note is back-linked (say from your daily notes), a reference will appear in *incoming backlinks*. This is super handy when pulling up call notes on a person, for example.

![incoming backlink](https://firebasestorage.googleapis.com/v0/b/reflect-prod.appspot.com/o/users%2FgjzQZB390LOY9DmlguxzrU6xaHw2%2Ff8256614312547b1a57de5d9483398b1?alt=media&token=ae63093f-14e2-4316-a014-fc525517f233)

On other other hand, clicking on a *tag* takes you to a list of notes containing that tag. For example, clicking on the `#person` tag shows you a list of all notes with that tag (i.e. all the people you've tagged in Reflect).

![clicking tag](https://firebasestorage.googleapis.com/v0/b/reflect-prod.appspot.com/o/users%2FgjzQZB390LOY9DmlguxzrU6xaHw2%2F119880e2bd754b3294d16f8ecdd85854?alt=media&token=9a6eaf54-ae26-4538-811c-506040ce99ee)