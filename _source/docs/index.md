---
title: Docs
layout: page
---

# Broadlist Docs

- List weights and
- Types of creators
- Booklist file format

## Broadscore

Broadscore is very simple, possibly silly, attempt to calculate a single, numeric representation of a book's critical reception.

Broadlist exists to help readers find good books. Broadscore is an effort to reduce that search to an absolute minimal effort.

### List Weights
A *list weight* is the term we use to describe the importance (or the reputation) of a list.

Every list that is added to Broadlist is assigned a *list weight* of one of the following:
- heavy
- normal
- light

Each weight is assigned a value (3 for heavy, 2 for normal, 1 for light).

### List Placements

A *list placement* is the term we use to describe where a book sits within a list. Every book added to every list on *Broadlist* is given a list placement of exactly one of the following:
- winner
- shortlist
- longlist
- verylonglist

There are some subjective editorial decisions that go into these categorizations, but in most circumstances the list placement is straightforward. Most lists will name a winner, and a shortlist, and a longlist.

Each placement is assigned a value (16 for a winner, 4 for a shortlist, 2 for a longlist, 1 for a verylonglist). We arrived at these numbers both systematically and arbitrarily, through some trial and error.

When these are not explicitly named, we usually follow these guidelines to assign a placement.

If no winner is named we will generally not assign a *winner* placement.

We will often infer a *shortlist* placement for lists that include 6 or fewer books.

We will often infer a *longlist* placement for lists that include between 7 and 20 books.

And we will often infer a *verylonglist* placement for lists that include more than 20 books.

### Calculating Broadscore

And that's really everything.

Take a book. For each list that includes that book, multiply the *list weight* value by the *list placement* value. Add up those numbers and you've successfully calculated a *broadscore*.

Every list that is added to Broadlist is assigned a *weight* which is meant to represent its importance.

As an example: let's say I have blog (*Matthew's Book Blog*, perhaps) and each year I post a list of my  favorite books. The post is titled something like *Matthew's Favorite Books of 2024*.

#### Example


### Notes

For our purposes here, a book has exactly one (1) list placement per list. Being assigned a *winner* placement does. Even though, logically, yes, the winner of a prize also made the longlist.

The idea here is that the book earns its broadscore value using its single, best (highest value) *list placement*.

### Critiques

Isn't this kind of made up and rather silly?

Maybe. Broadscore is almost certainly not the most accurate way to determine if a book is good. There will be lots of great books with a *broadscore* of exactly 0.

It aspires to be useful as a very fast way of determining if a book might be good.

We think it's more valuable at the high end - capturing books that win multiple awards, make multiple shortlists, and are critically relavent for a particular year.

A very blunt way to use broadscore:
- Broadscore of 0: do more research
- Broadscore of 50: probably pretty good, included in multiple lists
- Broadscore of 100: almost definitely an important book
