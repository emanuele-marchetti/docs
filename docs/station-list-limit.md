# You asked for a list, you got a list. It does not tell you how many there are.

**Applies to:** Paginated REST APIs | **Level:** Intermediate | **Time to resolve:** 10 minutes

You called the API and it gave you exactly the list you expected. Now you base your work on it.

How many stations are there really?

In this list you know what's there, not what isn't.

There is a cap on the number of stations in the response; it is called `limit`.

When there are more stations than the limit, you receive exactly `limit` stations. The rest is left out. No alert.

You cannot tell whether you have a complete list or one that just reached the `limit`.

Request the list one page at a time. As long as a page comes back full, you request the next. When a page comes back with fewer, you can assume you have reached the end.

Exactly. You asked for stations, and that is what you got. But you wanted all of them.

*Written by Emanuele Marchetti*
