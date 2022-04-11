# Reading the Tab List

The tablist in minecraft looks like this:

![Hypixel's Tab List](https://i.imgur.com/O40uL1W.png)

### Reading the Header and Footer...

So how do we read the `"You are playing on MC.HYPIXEL.NET"` and `"Ranks, Boosters & MORE! STORE.HYPIXEL.NET"` part?

There is a convenient object on the bot object called `bot.tablist`, this object has a `header` and a `footer` key on it which are [`ChatMessage`](https://github.com/PrismarineJS/prismarine-chat#chatmessagemessagedisplaywarning) objects.

[`ChatMessage`](https://github.com/PrismarineJS/prismarine-chat#chatmessagemessagedisplaywarning) objects have a [`.toString()`](https://github.com/PrismarineJS/prismarine-chat#chattostringlang) function on them that allows converting them to flat text.

```javascript
console.log(bot.tablist.header.toString()) // 'You are playing on MC.HYPIXEL.NET'
console.log(bot.tablist.footer.toString()) // 'Ranks, Boosters & MORE! STORE.HYPIXEL.NET'
```

Simple enough right? Just make sure that you call these functions at least after the bot spawns. This can be done by putting the code into a `spawn` event in mineflayer. Like so:

```javascript
const bot = createBot({...})

bot.once('spawn', () => {
    console.log(bot.tablist.header.toString()) // 'You are playing on MC.HYPIXEL.NET'
    console.log(bot.tablist.footer.toString()) // 'Ranks, Boosters & MORE! STORE.HYPIXEL.NET'
})
```

### Now, How do we read the players?

First, we need to know how to find the active players on the server. We have a [`bot.players`](https://github.com/PrismarineJS/mineflayer/blob/master/docs/api.md#botplayers) map of player -> player object.

So in order to get all the players, we just need to get all the players out of the `bot.players` map. We can do that using [`Object.values`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Object/values)`(bot.players)` which will give us an array of player objects.

These player objects have a convenient function `.nameOnTablist()`, which returns a [`ChatMessage`](https://github.com/PrismarineJS/prismarine-chat#chatmessagemessagedisplaywarning) object or null.

Knowing all that above, we can put some code together to list the players on the tablist like so:

```javascript
for (const player of Object.values(bot.players)) {
    const name = player.nameOnTablist()
    if (!name) continue
    console.log(name.toString())
}
```

This will print all of the names on the tablist like shown above.

As talked about above, this should only be done after the bot has called the `spawn` event. Putting this code into the spawn block like shown above will suffice.
