# Looking at a player

1. Find a method that can make the bot look at something.

&#x20;     Searching the phrase "look" on the bot in the PrismarineJS discord yields this output:

![](https://i.imgur.com/UPV5KJY.png)

2\. Finding a way to get the player's position

&#x20;   Mineflayer bot's have a `bot.players` object that points usernames to their `player` objects, so we can use that. The `player` object has a `player.entity` property, and the `entity` object has an `entity.position` property, which we can give to `bot.lookAt`

3\. Final Code:

```javascript
await bot.lookAt(bot.players[username].entity.position)
```
