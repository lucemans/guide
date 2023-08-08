---
setup: |
  import Layout from '../src/layouts/BlogPost.astro'
  import Person from '../src/components/person/Person.astro'
title: Scyllo, the Cassandra/Scylla library you didn't want but got anyways
type: package
date: 1634748007702
published: true
---

# Scyllo

<p>A short while ago a collegue of mine, <Person name="antony1060"/>, and I were working on a project together. The project in question used <a href="https://www.scylladb.com/" target="_blank">ScyllaDB</a> as a database, and throughout its lifecycle we found ourselves again and again writting wrapper functions for the database operations.</p>

## Deutsche Bahn
One day on my way back home from a family trip I decided to challenge myself, and attempt to combine all of the wrapper functions we had written into a simple, clean, yet effective, fully-typed library. And thus, [Scyllo](https://npmjs.org/package/scyllo) was born! 🎉

Ironically enough the German train transit system is called `Deutsche Bahn`, or, `DB` for short. Which, I, whilst writing a database library, found very humorous.

## Installation
Installation of scylla is relatively easy. Simply instruct your prefered package manager `npm` or `yarn` to add it and you should be good to go.
```
npm install scyllo
```
Or with `yarn`
```
yarn add scyllo
```

## How to use
Setting up a basic project using scyllo should be as easy as the following. First, in order to initialize our client, we need to have some types defined for the entities in our database. In this example we will be storing `Users` and `Blogposts`. Let's define those types.

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

Now let's initialize our client. Client initialization is as simple as creating the client and specifying the types. Inside of the client we will create a `DataTables` object, the object's keys are table names and the value should be the type of the entry in that table like so:

```js
{
	users: User,
	posts: Blogpost
}
```

After we understand how this works we can now make use of it to create the client as follows:

```ts
const DB = new ScylloClient<{
	users: User,
	posts: Blogpost
}>({
	client: {
		/* Insert your cassandra/scylla config here */
		/* Don't worry, typescript will help you out */
	}
});
```

After having created this client we store it in a variable, in my personal preference this variable is called `DB`, because it makes queries super fun to type. But in reality you can name this anything, `client`, `database`, `thatonethingthatssupposedtoworkgetmemydata`, or anything of the sorts.

### Making your first query

With your first query we will want to insert data into our database. Say a user signs up, we could create their user object, and then simply insert it like so:

```ts
const nUser: User = {
	user_id: '12345',
	username: 'lucemans',
	email: 'luc@lucemans.nl',
	dob: '12-34-5678'
};

DB.insertInto('users', nUser);
```

And thats how easy it is.

### Fetching information

Querying the database for data can be a lot more interesting tho, lets have a look.

```ts
const user = await DB.selectOneFrom('users', ['username', 'email'], {user_id: '12345'});
```

With the above code executed, a single user will be retrieved from the database for whom the `user_id` is equal to `'12345'`.

Need multiple users you say? Sure, why not, just use `selectFrom`

```ts
const users = await DB.slectFrom('users', ['username', 'email'], {password: '1234'})
```

### Deleting information

In CQL, the `DELETE` keyword is for both deletion of complete rows of data in tables, but also the deletion of certain columns. Both can be done through the same function within scyllo. Lets give that a try aswell:

Deletion of an entire row:

```ts
await DB.deleteFrom('users', '*', {user_id: '12345'})
```

Deletion of just a single column

```ts
await DB.deleteFrom('users', ['password'], {user_id: '12345'})
```

## Finalization

I hope that the above post has made you somewhat interested in scyllo, scylla, cassandra or anything else related. And it inspired you to do some crazy stuff. Obviously it is upto you what you want to do. There are a fair bit of alternatives out there for other database types such as sequelize, typeorm, prisma, and more.

If you are however interested in scyllo, feel free to check out these:

[Scyllo Github](https://github.com/lvkdotsh/scyllo)

[Scyllo NPM](https://npmjs.org/package/scyllo)

~Luc
