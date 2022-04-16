# Finding items in bot's inventory

![Typical Minecraft inventory](https://i.imgur.com/0HbPRbX.png)

So you want to know what's in the bot's inventory... This is a very easy because of the [`prismarine-window`](https://github.com/PrismarineJS/prismarine-windows) integration.

### Finding if you have any iron swords in your bot's inventory

1. Take a look at your bot's `bot.inventory` object, which will be used extensively when interacting with the inventory.
2. Find the item id of an iron sword using `bot.registry` for more info take a look at the Using Minecraft-Data article.
3. `bot.inventory.items()` can be used to get all items that are in the blue glass, red glass, and the sword slot as an array, just [filter it](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Array/filter) down.

The final code should look like this:

```javascript
const ironSwordId = bot.registry.itemsByName.iron_sword.id
const ironSwords = bot.inventory.items().filter(item => item?.type === ironSwordId)
const itemCount = ironSwords.reduce((acc, swordStack) => acc + swordStack.count, 0)
console.log(`Bot has ${itemCount.length} iron swords!`)
// For counting the number of items in the inventory of a stackable item, this can be used
const steakCount = bot.inventory.count(bot.registry.itemsByName.steak.id)
console.log(`Bot has ${steakCount} steak`)
```
