---
setup: |
  import Layout from '../src/layouts/BlogPost.astro'
  import Person from '../src/components/person/Person.astro'
title: Sunflake, Zero dependency, lightweight, snowflake generator
description: Sunflake is a Zero dependency, lightweight, snowflake generator
type: package
date: 1641087405492
published: true
---

# Sunflake

Whilst creating a multitude of projects I have always noticed that I had to generate IDs for database entries. Wether it be users, blogposts, orders, or anything else, IDs are always important.

Now with my recent switch to using [Scyllo](https://github.com/lvkdotsh/scyllo) (and thereby [Scylla](https://www.scylladb.com/)), which, to add to the conversation, does not generate IDs itself, I have started to look into solutions.

After stumbling upon the [Snowflake ID](https://en.wikipedia.org/wiki/Snowflake_ID), which is currently what is utalized by platforms such as [Discord](https://discord.com/developers/docs/reference#snowflakes), [Twitter](https://blog.twitter.com/engineering/en_us/a/2010/announcing-snowflake), [Instagram](https://instagram-engineering.com/sharding-ids-at-instagram-1cf5a71e5a5c) and [Blizzard](https://techcrunch.com/2010/10/12/twitter-snowflake/) just to name a few, I realized we might have a winner.

After further testing and using it in a few projects (using [flakeid](https://npmjs.com/package/flakeid)) it appeared to work nicely.

## Why Sunflake?

<p>Whilst (ironically) on Discord (which uses Snowflakes thats why its funny), <Person name="robiot" /> and I further discussed Snowflakes, Gen-Z Snowflakes, and how to get better typescript support. This is when <a href="https://github.com/lvkdotsh/sunflake" target="_blank">Sunflake</a> came into the picture.</p>

<o><Person name="robiot" /> and I then proceeded to re-implement <a href="https://en.wikipedia.org/wiki/Snowflake_ID" target="_blank">Snowflake ID</a> natively in typescript.</p>

## Installation
Installation of sunflake is relatively easy. Simply instruct your prefered package manager `npm` or `yarn` to add it and you should be good to go.

```shell
npm install sunflake
```
Or with `yarn`
```shell
yarn add sunflake
```

## How to use

Using Sunflakes requires one setup function to be ran. In this function we can specify the `MachineID` aswell as the preferred `Epoch` timestamp to use.

| Option | Description |
| :- | :- |
| Machine ID | Number used to differentiate one machine/process from another. |
| Epoch | Custom timestamp at which the universe was created<br> or whatever steve decided, upto u. |

```ts
import { generateSunflake } from 'sunflake';

const snowflake = generateSunflake({
    machineID: 1, // Machine id
    epoch: 1640995200000 // First of January 2022
});
```

Now when you are ready to generate a snowflake, run it as follows.

```ts
const randomId = await snowflake();
```

And voila! In addition if you wanted to generate it for a specific timestamp, you could do the following

```ts
const time = new Date('2022-01-02').getTime();
const randomId = await snowflake(time);
```

## Why Snowflake ID

Snowflakes are awesome, they incorporate the current timestamp when generated (in the first 42 bits), then the next 10 bits are used to differentiate between instances, and the last 12 bits for a millisecond sequence counter.

This essentially mittigates that, if a multitude of processes tried spawning a lot of snowflakes at the same time, would ever produce overlapping IDs.

In addition to the values being `time-based`, this also allows IDs to be in cronological order if sorted/queried. This `time-based` ID spec allows for (in Discord's case) easy fetching messages that were generated between two specific timestamps.

## Finalization

I hope that the above has peaked your interest for ID generation as much as it has for me. And next time you are working on IDs think about what you are using and choosing to go for.

If you would like to try out sunflake, check out these links:

[Sunflake on Github](https://github.com/lvkdotsh/sunflake)

[Sunflake on NPM](https://npmjs.org/package/sunflake)

~Luc
