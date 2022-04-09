# Starting your mineflayer bot

## 0. Getting Help

If at any point in this guide something doesn't make sense, or you get different output then is expected by the guide, feel free to join the [mineflayer discord](https://discord.gg/GsEFRM8) and ask in #help

## 1. Make a folder

No really, make a folder, and make a file called `index.js` into the folder.

## 2. Installing Mineflayer

Open the folder you made within a terminal, and run these command:

`npm init`

`npm install mineflayer`

## 3. Make a hello-world application

Open your index.js file, and put the following code into the file

```javascript
const mineflayer = require('mineflayer')
const bot = mineflayer.createBot({
  host: 'mineplex.com',
  username: 'myemail@gmail.com',
  auth: 'microsoft'
})

bot.once('spawn', () => {
    console.log('I have spawned!')
})

bot.once('error', (error) => {
    console.log(error)
})

bot.once('kicked', (kickMsg) => {
    console.log(kickMsg)
})
```

## 4. Starting the application

To start the application, simple run `node index.js` in your terminal. You should get output that looks like the following:

```
PS C:\Users\---\Documents\js-projects\docs-bot> node index.js
[msa] First time signing in. Please authenticate now:
To sign in, use a web browser to open the page https://www.microsoft.com/link and enter the code BTGEAU9U to authenticate
```

Follow the link and enter the code. then click the button. Then you should see in you console:

`I have spawned!`

Now you have successfully started your mineflayer bot.
