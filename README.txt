READ ME

Dad -

So, you found the Writing folder!

Awesome. There are some moving parts here that warrant explanation.

First and foremost, this structure is NOT set in stone.
I just whipped up the directory pattern off the top of my head.
If you want it different, make it so.


Second, Git. No, not "Git outta here". Git.

Git is Version Control.
It lets you save a version of a document "to the cloud".

Key word is *Version*. You're not only saving your document, as it is right now,
but a version of it, along with its place in the timeline.

Example: Pretend you're Lewis Carrol.
On January 1st, you create document "Jabberwocky.txt".

Inside, you write the first stanza of The Jabberwocky:
"Beware the Jabberwock, my son!
  The jaws that bite, the claws that catch!
Beware the Jubjub bird, and shun
  The frumious Bandersnatch!"

Lovely. You decide to get some rest and finish it later, so you save to your
hard drive and go to sleep.

When you wake up, you open up Jabberwocky.txt and there it sits, ready to continue.
So you write out the second verse:
"He took his vorpal sword in hand:
  Long time the manxome foe he sought --
So rested he by the Tumtum tree,
  And stood awhile in thought."

Save it, and go for a walk.

Any time you open it, you open the last save, and any time you save it,
you overwrite the previous save. This is the core function of files.

Create file -> Write to file -> Save
Open -> Read -> Overwrite -> Save
Or you can save the new version as a copy.

So what happens if you open "Jabberwocky.txt", select all the text, delete it,
and click save?

Well, it's gone. POOF! By the nature of files, you've effectively deleted all
that text. It's gone. The file did its job - it wrote down your most recent save.

It doesn't care if that save had bad grammar or no content. It just does what it's told.

Enter Undo.
You're probably thinking "Oh, that's what undo is for", and you're exactly right.
Undo, when implemented properly, watches all the changes you make to a document while it's open,
then saves the last hundred or so actions in a timeline, so you can go back and NOT delete all your stuff.

That's great. It's amazing, really. Buuuut... as soon as you close the file,
or the program that currently has it open, all your undo history evaporates.

So if you select all the text, delete it, save it, then close the file, you're out of luck.

There's no way to track all the history of that file. The application-specific Undo history
is... well, it's application specific. Closing the file or closing the application deletes it.

The actual file itself is just CURRENT VERSION. It has no support for "What I used to be 5 minutes ago",
because that isn't the job of a file.


Enter Git.

VERY simply put, Git is undo for a file. Better yet, for an entire directory.
It's not saving.
It's not undo.
It's Version Control.

Here's how it works.

You've got an empty folder, "Poems".
On January 1st at 8am, you add an empty text file and save it as "Jabberwocky.txt"

Then, because you use Git, you "Commit" the "Poems" folder in its current state.

What it does is take a "snapshot" of everything inside that folder,
and saves it "somewhere else" - generally to a hidden folder deep in your system
that you can't (and don't want to) access.

At 8:30, you finish the first stanza. You put it inside "Jabberwocky.txt", save it,
and commit it.

Now Git has two versions of this item: 8am and 8:30am. It's smart, so it knows
the 8:30am version is a child of the 8am version - its the same stuff, with changes.
Better yet, it *figures out what's different* and *lets you visually compare*.

So if you did a "Diff" of the 8am and 8:30am versions, it would show
8am:
File Jabberwocky.txt:
"" (blank)
8:30am
File Jabberwocky.txt:
"Beware the Jabberwock, my son!
  The jaws that bite, the claws that catch!
Beware the Jubjub bird, and shun
  The frumious Bandersnatch!"

4 lines changed

Then you could choose.

Let's say you (Lewis) are really torn: You're considering naming the monster
"WabberJocky" instead.

So you create a new *Branch* and call it WabberJocky.

Now there are two branches: Master (default) and WabberJocky.

Anything that happens on the WabberJocky branch stays on the WabberJocky branch.

It starts out as an exact clone of the current directory:
Poems, JabberWocky.txt, and that's it.

So at 9am you open up JabberWocky.txt in your new branch, replace all the instances of "JabberWocky" with
"WabberJocky", save and commit.

Now there are 3 versions of the file, split across 2 branches.

Master:
8am version -> 8:30am version

WabberJocky
9am version (Child of Master Branch's 8:30 Version)

Now, you could go and rewrite the poem in both branches.

Or you could do a Diff between them and *Choose*.

The Diff will look like:

Master 8:30am:                                   WabberJocky 9:00am
>>> "Beware the Jabberwock, my son"              "Beware the WabberJock, my son!
  The jaws that bite, the claws that catch!         The jaws that bite, the claws that catch!
Beware the Jubjub bird, and shun                 Beware the Jubjub bird, and shun
>>>  The frumious Bandersnatch!"                      The frumious Bandersnatjach!"


Here, the ">>>" denotes a line with changes. In this case, there's a line we didn't mean to change!
ACK! Looks like we accidentally inserted some characters into the last line.
Thanks to Git, we can catch that change. Simple as that.

Then we can choose the version we want.
Perhaps we like WabberJock, but don't want the typo.

So we Merge WabberJocky back into the Master.
When we do, it has problems, because there are differences. It needs a human to decide which one is right.
So we choose the first line from WabberJocky 9:00am, "Beware the WabberJock, my son!"
But we choose the fourth line from Master 8:30am, "The frumious Bandersnatch!"

And it's okay with that. It's really good at it!
Then it'll just commit the new version to master, and remove the branch (without deleting its history) by merging it into master's history!



Okay WAIT STOP TOO IN DEPTH.
Why the heck do you care?

1) Git has easy tools that let you take a structured directory and share it.
2) There are a billion+1 ways to take static files from Github and serve them up as web components. So that "Poetry" folder
very easily, with just a few lines of code, becomes data that feeds a "Poetry" page on a website.
If the data is sourced from Github, and you're Committing changes to Github, then the page updates when the files do.
This means (once the frontend is set up) that adding an entire poem or chapter is Just One Step.

The way it normally works is Master is SACRED. Only good, edited, Publish-ready content goes there.
Everything else happens in a branch.
So you get struck by an idea for a poem about Dancing Bees (I don't know, just making stuff up).
You create a branch "DancingBees".
Create a file in Poetry, call it "DancingBees.txt".
You write half of it, save and commit.
Git holds onto the branch. Because it is NOT in master, your half-finished poem doesn't go public.

You finish the poem, commit that, and merge it back into master.
Since there are no other changes in the directory (You've created a new file - that doesn't cause conflict),
Git happily merges everything. It knows all the other files are the same, so it just adds DancingBees.txt to its record.

Since that's now on Master, it gets to the website. Boom!
