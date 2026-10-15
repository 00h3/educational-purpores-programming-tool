.

### - Setup Config Files -

Once you download the project files you will see a folder named `config`. Inside of it will be 4 files and 1 folder:

- `avatars`
- `config.json`
- `games.json`
- `keywords.json`
- `paste.json`

#### `avatars`

This is the folder where you drag and drop your avatar images if you enabled avatar rotating.

#### `config.json`

This is the main config file. Inside you will see several options. This is what each one means:

- `token` is your Discord token. (if you don't know what a Discord token is, or how to get yours, [**check out this tutorial made by me**](https://github.com/TheRacingLion/Discord-SelfBot/wiki/Discord-Token-Tutorial))
- `ownerID` is your discord ID
- `prefix` is the desired prefix for bot commands (can use `@mention ` if you want the prefix to be your Discord mention)
- `rotatePlayingGame`, if you want your Discord playing game to rotate games (from the `games.json` file)
- `rotatePlayingGameTime`, if you do want the game to rotate, this is the time interval you want for it (in milliseconds)
- `rotatePlayingGameInStreamingStatus`, if you do want the game to rotate, if you want it to rotate in streaming status
- `rotateAvatarImage`, if you want your Discord avatar image to rotate (from the images in `config/avatars` folder)
- `rotateAvatarImageTime`, if you do want the avatar to rotate, this is the time interval you want for it (in milliseconds)
- `defaultStatus`, the default Discord status to show on your account. Either "online", "idle", "dnd" (Do Not Disturb) or "invisible"
- `mentionNotificator` (if you want to have your mentions notified)
  + `inConsole` (as a log to console)
  + `inNotificationChannel` (as a message sent to the notification channel)
  + `logBlockedUsers` (if you want users you blocked to be logged or not)
  + `ignoredServers` (an array of server ID's you want the bot to ignore when searching for mentions)
- `keywordNotificator` (if you want to have specific keywords notified)
  + `inConsole` (as a log to console)
  + `inNotificationChannel` (as a message sent to the notification channel)
  + `logBlockedUsers` (if you want users you blocked to be logged or not)
  + `caseInsensitive` (if you want the bot to search for the keywords while paying attention to the letter case or not)
  + `ignoredServers` (an array of server ID's you want the bot to ignore when searching for keywords)
- `eventNotificator` (if you want to have events like guild creations, or friend requests notified)
  + `inConsole` (as a log to console)
  + `inNotificationChannel` (as a message sent to the notification channel)
- `notificationChannelID`, if you set `inNotificationChannel` to `true` at least once, the channel ID to make notifications in
- `defaultEmbedColor` is the hex color code for the default color for embeds
- `deleteCommandMessages` if command messages and error messages should be deleted after a bit
- `deleteCommandMessagesTime` if you do want the command messages deleted, this is the time the bot should wait before doing it (in milliseconds)
- `PSN` PSN Status setup
  + `enabled` (if you want to use PSN Status reporting)
  + `email` is your PSN email
  + `password` is your PSN password
  + `psnid` is the PSN ID you want to report on
- `XBOX` XBOX Status setup
  + `enabled` (if you want to use XBOX Status reporting)
  + `gamertag` is the XBOX Gamertag you want to report on
  + `apikey` is your apikey from http://xboxapi.com sign up for a free account

#### `games.json`

This is where the game names you want to use for the rotating playing game option are. To add or delete games, just follow the structure of the games that are already on it. (If you have set the `rotatePlayingGame` option in the `config.json` file to `false`, then you dont need to worry about this file)

#### `keywords.json`

This is where the keywords that you want the bot to search for go in. (If you have set the `keywordNotificator` options in the `config.json` file to `false`, then you dont need to worry about this file)

#### `paste.json`

This file is where the meme texts are stored for the `paste` command, if you wish to add more to use with `paste` just follow the structure of the file and add them in. If an array is specified for one of the options then the bot will choose a random item from the array.

### - Start the bot -

When you have the required programs installed, have all project files, and have setup config files, you can start the bot:

#### Windows

Open the `installer.bat` file. This will install the required node modules (so you dont have to do it yourself) and create a `run.bat` file. You can use this file to start the bot. If you did everything correctly, the bot should start up fine.

If for some reason you have ran `installer.bat`, it disapeared and it didnt create `run.bat`, then re-download `installer.bat` and try again. Most likely either git or node were not installed correctly. Check if they work and try again.

#### Linux / Mac

Executable files are kind of weird in Linux, and users most likely use console to do their work, so to setup this selfbot on linux or mac open a terminal in the directory you downloaded the files to and type `npm i`. Once it is finished you can start the selfbot by using `npm start` or `node self.js`. If you did everything correctly, the bot should start up fine.

# Commands

All commands get logged to console, are case insensentive and are tested to see if the owner of the bot was the one who triggered the command. It should be easy to create commands if you know the basics of JavaScript. The library used is [**Eris**](https://abal.moe/Eris/docs/CommandClient#function-registerCommand).

### - Default Commands -

The bot has several default commands. (Each command is explained inside their own file.) You can find a detailed command list [**here.**](https://github.com/TheRacingLion/Discord-SelfBot/wiki)

### - Creating Commands -

When you want to create a new command, just add a new file to the `commands` folder and name it something like `mycommand.js` and then follow the basic structure below. If your command needs some kind of special options like permissions or you just want to set it to be used on guilds only, then you can use the pre-made command options shown below. There are also some helper functions built in to the function.

```js
/*
  Optional comment string to describe the command.
*/
module.exports = (self) => {
  self.registerCommand('mycommand', function (msg, args) {
    // Do something with msg or args

    this.send(msg, 'This is some text', deleteDelay) // Send a message

    this.embed(msg, { // Send an embed
      title: 'Embed title',
      description: 'Embed description',
      color: 4627433
    }, deleteDelay)

    this.findMember(msg, args[0]) // Find a guild member
  }, {
    noPms: false, // Will only work on guilds (No PM's)
    aliases: ['cmd', 'mycmd'], // Will make "cmd" and "mycmd" be an alias of "mycommand"
    perms: [ // Will only do the command if you have the "Manage channels" AND the "Manage Nicknames" permissions
      'manageChannels',
      'manageNicknames'
    ],
    deleteAfter: false // Delete the command message after the command was done or not
  })
}
```

### - Logging -

The selfbot comes with its own logger file, which includes a few options to log things to console. If you know what you are doing, you can add many more. It uses [**Chalk**](https://www.npmjs.com/package/chalk#colors) to change the color of the logged text, so you can change the colors if you do not like them.

#### Normal Logs

If you just want to log text to console, you can do:
```js
log.log('Text you want to log', 'Logger title', 'Chalk color that you want for the logger title', timed)
/*
  Logger title is optional
  Check all chalk colors at https://www.npmjs.com/package/chalk#colors
  "timed" is either true or false. Adds a timestamp to the log. (Default is false)
*/
```

#### Warning Logs

If you want to log a warning to console, you can do:
```js
log.warn('Something weird but non-breaking happened', 'Warning origin')
// Warning origin means the place where the warning came from (optional)
```

#### Error Logs

If you want to log errors to console, you can do:
```js
let err = 'This is an error'
log.err(err, 'Error origin')
// Error origin means the place where the error came from (optional)
```

# License

[MIT](LICENSE). Copyright © 2016, 2017, 2018 [TheRacingLion](https://github.com/TheRacingLion).
