# LEFT JOIN: why your rows disappear when you filter in the WHERE clause

**Applies to:** SQL | **Level:** Intermediate | **Time to resolve:** 2 minutes

## The rule

In a LEFT JOIN, a condition on the optional side of the join belongs in the ON clause, not the WHERE clause.

## The scenario

You need a complete list of names from the Authors table and any corresponding books from the Books table, pairing authors with books, but including only titles from 1957.

## The query that looks correct

This is the query we would probably write. It looks valid, but it does not return the results you want.

```sql
SELECT a.name, b.title
FROM authors a
LEFT JOIN books b ON b.author_id = a.id
WHERE b.year = 1957;
```

| name    | title              |
|---------|--------------------|
| Calvino | Il barone rampante |

## The result

The result is a shorter list that does not include every author; the authors who are present all have at least one book from 1957. The WHERE clause filtered out the rows that would have displayed authors with no books from 1957.

## The reason

It is a matter of sequence. The WHERE clause comes into play after the query has already generated an initial list containing authors who do not have books from 1957. It operates on that list, removing rows for authors where the publication year value is missing because, effectively, NULL does not satisfy the condition `= 1957`.

## The solution

Therefore, the condition needs to be moved earlier in the sequence; this can be done by using the ON clause, which operates at the JOIN level, and thus prior to the WHERE clause. With this syntax, authors who do not have a corresponding book written in 1957 remain in the list rather than being discarded later.

```sql
SELECT a.name, b.title
FROM authors a
LEFT JOIN books b ON b.author_id = a.id AND b.year = 1957;
```

| name     | title              |
|----------|--------------------|
| Calvino  | Il barone rampante |
| Ginzburg | NULL               |
| Levi     | NULL               |
| Morante  | NULL               |

*Written by Emanuele Marchetti*
