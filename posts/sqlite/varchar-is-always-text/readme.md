---
title: Do you know that if you're using VARCHAR(10) on SQLite you can store 1-million characters anyway?
published: true
description: VARCHAR is TEXT type on SQLite database
tags: 'sqlite, varchar, text, length'
cover_image: ../assets/cover.jpg
canonical_url: null
id: 976317
---

###### :postbox: Contact :brazil: :us: :fr:

[Twitter](https://twitter.com/campelo87)
[LinkedIn](https://www.linkedin.com/in/flavio-campelo/?locale=en_US)

---

## SQLite is typelessness

Yes, it's true! According to [SQLite dataypes documentation](https://sqlite.org/datatypes.html), except only one exception, you can store any kind of data you want in any column of any table, regardless of the type declared datatype of that column. The only exception are **INTEGER PRIMARY KEY** columns. So, you can pay attention for that.

## Warning for automated testing

If you have automated tests and you think that all of your code is working with SQLite, maybe you should to consider making some tests and running them on your server databases (MSSQL, Oracle, PostgreSql, etc.).

When you use datatypes like **CHAR, VARCHAR, BLOB, CLOB** all of them will be **TEXT** datatype having **UNRESTRICTED** length how you can find [here](https://www.sqlite.org/datatype3.html). 

> (ex: "VARCHAR(255)") are ignored by SQLite - SQLite does not impose any length restrictions (other than the large global SQLITE_MAX_LENGTH limit)

Look at this sample: 

```SQL
CREATE TABLE MyTable(
    MyColumn VARCHAR(3)
);
```

You should keep in mind that it will work differently using SQLite and any other databases. So, if we try this query bellow in a Oracle DB, it won't work.

```SQL
INSERT 
    INTO    MyTable (MyColumn) 
    VALUES  ("my string with more than 3 characters");
```

But if you use the same query on a SQLite DB, it will work perfectly.

## Conclusion

It's always important to know how a tool works to avoid future problems or, at least, you can ready if they arrive. 

I'm here only to share with you some of new things that I find working. I hope that is as important to you as it was for me.

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.