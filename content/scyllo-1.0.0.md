---
setup: |
  import Layout from '../src/layouts/BlogPost.astro'
  import Person from '../src/components/person/Person.astro'
title: Scyllo reaches v1.0.0 🎉🥳
permalink: https://luc.computer/p/scyllo-1.0.0
description: A post about scyllo or whatever
slug: scyllo-1.0.0
type: package
date: 1641091223207
published: true
---

# Scyllo v1.0.0 🎉🥳

<p>A short while ago, <a href="https://github.com/lvkdotsh/scyllo" target="_blank">Scyllo</a> was born. Together with the help of <Person name="svemat" />, <Person name="antony1060"/> and <Person name="joshhendrix" />, we have managed to take this project to the next level. By design, Scyllo works out of the box with Typescript Types, aswell as with <a href="https://www.scylladb.com/" target="_blank">ScyllaDB</a>.</p>

So let's get to it already, what makes this library so awesome?!?

## Installation
Installation of scylla is relatively easy.
Simply instruct your prefered package manager `npm` or `yarn` to add it and you should be good to go.
```
npm install scyllo
```
Or with `yarn`
```
yarn add scyllo
```

## Setup
Setting up Scyllo is as easy as pie. First initialize some types for objects we want to be storing. We will create `User` and `Blogpost` as follows:

```ts
type User = {
	user_id: string;
	username: string;
	email: string;
	dob: string;
};

type Blogpost = {
	blog_id: string;
	title: string;
	content: string;
	author_id: string;
	publish_date: number;
};
```

Keep in mind that in the above example we are using `type`, you could also use `interface` or `class` definitions.

Now let's initialize the Client!

```ts
const DB = new ScylloClient<{
	users: User,
	posts: Blogpost
}>({
	client: {
	    contactPoints: ["localhost:9042"], // Where to access the database
	    keyspace: "mykeyspace", // Default keyspace
	    localDataCenter: "datacenter1", // Local Datacenter
	}
});
```

## Next Steps
Now that we have created the client we can run a variety of functions on our database to just list a few:

  - [selectFrom](https://github.com/lvkdotsh/scyllo#selectfrom)
  - [selectOneFrom](https://github.com/lvkdotsh/scyllo#selectonefrom)
  - [insertInto](https://github.com/lvkdotsh/scyllo#insertinto)
  - [deleteFrom](https://github.com/lvkdotsh/scyllo#deletefrom)
  - [update](https://github.com/lvkdotsh/scyllo#update)
  - [createTable](https://github.com/lvkdotsh/scyllo#createtable)
  - [dropTable](https://github.com/lvkdotsh/scyllo#droptable)
  - [truncateTable](https://github.com/lvkdotsh/scyllo#truncatetable)
  - [createIndex](https://github.com/lvkdotsh/scyllo#createindex)
  - [createLocalIndex](https://github.com/lvkdotsh/scyllo#createlocalindex)
  - [createKeyspace](https://github.com/lvkdotsh/scyllo#createkeyspace)
    - [dropping a keyspace](https://github.com/lvkdotsh/scyllo#dropping-a-keyspace)
  - [useKeyspace](https://github.com/lvkdotsh/scyllo#usekeyspace)
  - [awaitConnection](https://github.com/lvkdotsh/scyllo#awaitconnection)
  - [shutdown](https://github.com/lvkdotsh/scyllo#shutdown)
  - [raw / rawWithParams](https://github.com/lvkdotsh/scyllo#raw--rawwithparams)
  - [query](https://github.com/lvkdotsh/scyllo#query)


## Finalization

With all of these crazy things above, fully typed using generics, tested using jest, and object-mapped to and from its javascript equivalents it has become a library as easy to use as a document database, but the performance of an in-memory, and the flexibility of your average relational. Yes, it might be a bit of a mess, but it is a hell of a good one to say the least.

For more information about Scyllo, check these links out:

[Scyllo Github](https://github.com/lvkdotsh/scyllo)

[Scyllo NPM](https://npmjs.org/package/scyllo)

~Luc
