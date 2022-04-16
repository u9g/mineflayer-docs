# Drop item's in bot's inventory

![](https://i.imgur.com/RVAfS7X.png)



So you're bot has been working for a while now, how do you drop the items to a player now?

### Dropping all stone in the bot's inventory

1. First, you will want to listen to chat for a message in which you will tell the bot to drop it's items in your direction.

```javascript
const bot = createBot([...])

bot.on('chat', async (username, msg) => {
    if (msg !== 'drop items') return
    // look at the player
    bot.chat(`I am now looking at you, ${username}`)
})
```

2\. To look at the player, take a look at [looking-at-a-player.md](../common-tasks/looking-at-a-player.md "mention")&#x20;

&#x20;    Now that we have the code for looking at the player, we can add that to our bot's chat listener:

```javascript
const bot = createBot([...])

bot.on('chat', async (username, msg) => {
    if (msg !== 'drop items') return
    await bot.lookAt(bot.players[username].entity.position)
    bot.chat(`I am now looking at you, ${username}`)
})
```



3\. To find what items to drop, take a look at [simple-inventory-interaction.md](simple-inventory-interaction.md "mention")

With that added, our code will now look like this:

```javascript
const bot = createBot([...])

bot.on('chat', async (username, msg) => {
  if (msg !== 'drop items') return
  await bot.lookAt(bot.players[username].entity.position)
  bot.chat(`I am now looking at you, ${username}`)
  const cobblestoneId = bot.registry.itemsByName.cobblestone.id
  const cobblestoneStacks = bot.inventory
    .items()
    .filter(item => item?.type === cobblestoneId)
  bot.chat(`I am about to drop ${cobblestoneStacks.length} stacks of cobblestone`)
})
```

4\. Finally, we have to loop through those items, and call [`bot.tossStack`](https://github.com/PrismarineJS/mineflayer/blob/master/docs/api.md#bottossstackitem) on the stacks of items

```javascript
const bot = createBot([...])

bot.on('chat', async (username, msg) => {
  if (msg !== 'drop items') return
  await bot.lookAt(bot.players[username].entity.position)
  bot.chat(`I am now looking at you, ${username}`)
  const cobblestoneId = bot.registry.itemsByName.cobblestone.id
  const cobblestoneStacks = bot.inventory
    .items()
    .filter(item => item?.type === cobblestoneId)
  bot.chat(`I am about to drop ${cobblestoneStacks.length} stacks of cobblestone`)
  for (const stack of cobblestoneStacks) {
    await bot.tossStack(stack)
  }
})
```

### Similar tasks

#### Dropping all items in a players inventory

This is exactly the same as done above, except we no longer have to filter the items, since we want to drop everything in the bot's inventory

```diff
const bot = createBot([...])

bot.on('chat', async (username, msg) => {
  if (msg !== 'drop items') return
  await bot.lookAt(bot.players[username].entity.position)
  bot.chat(`I am now looking at you, ${username}`)
  const cobblestoneId = bot.registry.itemsByName.cobblestone.id
  const cobblestoneStacks = bot.inventory
    .items()
-   .filter(item => item?.type === cobblestoneId)
  bot.chat(`I am about to drop ${cobblestoneStacks.length} stacks of cobblestone`)
  for (const stack of cobblestoneStacks) {
    await bot.tossStack(stack)
  }
})
```
