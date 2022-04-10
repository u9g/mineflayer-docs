# Simple inventory interaction

![Typical Minecraft inventory](https://i.imgur.com/0HbPRbX.png)

So you want to know what's in the bot's inventory... This is a very easy because of the [`prismarine-window`](https://github.com/PrismarineJS/prismarine-windows) integration.

### Finding if you have any iron swords in your bot's inventory

1. Take a look at your bot's `bot.inventory` object, which will be used extensively when interacting with the inventory.
2. Find the item id of an iron sword using `bot.registry` for more info take a look at the Using Minecraft-Data article.
3. `bot.inventory.items()` can be used to get all items that are in the blue glass, red glass, and the sword slot as an array, just [filter it](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/filter) down.

The final code should look like this:

```javascript
const ironSwordId = bot.registry.itemsByName.iron_sword.id
const items = bot.inventory.items()
const ironSwords = items.filter(item => item?.type === ironSwordId)
console.log(`Bot has ${ironSwords.length} iron swords!`)
```

