---
layout: post
title: SQL Server is a Document Database Too
permalink: 2012-12-19-sql-server-is-a-document-database-too.html
---

I know what you are thinking, "that sounds crazy". Sorta, but actually it's more common than you might think. A while back when I started exploring document databases and enjoying the benefits of using them, I started using a new and hip document db that was supposed to be awesome. At first it was. Then I started running into bugs, replication issues, etc, etc. 

Running into issues every so often and experiencing other oddities caused me to fear putting such a database into production. Of course I did it anyway. The results were mostly positive. Performance was good, and development was great, but oddities still surface every now and then. So I decided I need to move to a more proven database and being in the .NET space I chose SQL Server.

Eventhough I wanted to move to SQL Server, I didn't want to move to the relational model. I instead decided to use the exact same document model with a SQL Server backend. In a way this is nothing new like most things. I recall previously hearing about someone using MySql as a key-value store so why not SQL Server as a document store.

I started by creating a table for each type of document with an id field and a string field to hold the JSON serialized document data. This worked great except for how do I query the data? In the previous document database I was using, indexes were created based on what queries were wanted. Genius. I could do the same thing by just adding columns for the fields I wanted to query on.

A example might look like this.

Table: BOOK

<table>
	<tr>
		<th>Id</th>
		<th>Document</th>
		<th>Author</th>
	</tr>
	<tr>
		<td>1234</td>
		<td>{...}</td>
		<td>Joe</td>
	</tr>	
	<tr>
		<td>5678</td>
		<td>{...}</td>
		<td>Jane</td>
	</tr>
</table>

Basically we have the book document and a index for the author. The nice thing about these indexes is they can be added, removed, and reindexed at will. The only issue I've run into so far using this approach is when you want to index multiple values for a field that is perhaps a list of something. For instance, if you have a tags field in your document that contains a list of tags, it is possible to index this in a single column, but not optimal. In those cases it seems like you would need a seperate table for the index, but I haven't gone down that route yet.

The end result was a more reliable solution and surprisingly faster solution.