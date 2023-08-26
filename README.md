# rb-rologs-discord-message-sender

The RoLogs Discord Message Sender is a simple drop in LUA file that allows you to call discord web hooks directly from your own Roblox game.

First you need to purchase a token from the RoLogs discord channel. You can purchase for a given time frame.. e.g. 1 day, 1 week, 1 month.. or longer. To build the token RoLogs will ask you for the Discord webhook URL that you wish to use. You will need one token per Discord webhook that you want to use.

## Deliverables

Once a purchased you will receive:

- A token - the token has an expiry period. You will be told the exact UTC date of expiry. You will need to purchase a new token before the existing one expires - otherwise you will receive an error message. You can choose the duration and pay accordingly. Longer durations are cheaper.

- DiscordMessenger.lua - A lua file that you will drop into Roblox Studio. The file is obfuscated. Please note, the token expiry checking etc is done on the backend server, so there is no way to reverse engineer the lua code to bypass it.

<br/>

## Example

The following example shows how messages can be sent to Discord based on some in game events.

<br/>

### Step 1 - Create Classic Baseplate

In Roblox Studio create a new Classic Baseplate game.

<br/>

### Step 2 - Enable "Allow HTTP Requests" in your game

Turn on "Allow HTTP Requests"

You can turn on in game settings https://create.roblox.com/docs/studio/game-settings

Or via the "Command Bar" view by typing and and running:

```
game:GetService("HttpService").HttpEnabled = true
```

<br/>

### Step 3 - Drop in DiscordMessenger.lua 

- Click the + icon to the right of the "ServerScriptService" node.
- Search and add in "ModuleScript"
- Rename the new module script to be "DiscordMessenger" (i.e. right click the node and select rename)
- Open the module script by double clicking it
- Copy and paste all the contents of the provided file "DiscordMessenger.lua" into the "DiscordMessenger" editor window in Roblox Studio
- Click the + icon to the right of the "ServerScriptService" node.
- Search and add in "Script"
- Paste in the following code into the new Script - Note, for now leave the token value as "some_invalid_token". We will change that later.

<br/>

```lua
local SendDiscord = require(game:GetService("ServerScriptService"):WaitForChild("DiscordMessenger"))

local myToken = "some_invalid_token"

SendDiscord(myToken, 'This is my first test message in discord - this means the game started up!')
```

<br/>

Now run your game and look at the output window. You should see something similar to the below:

```
Create discord client!  -  Server - DiscordMessenger:1
*********************************************************************  -  Server - DiscordMessenger:1
* Unauthorized! - You need to request a token from the rologs group *  -  Server - DiscordMessenger:1
*********************************************************************  -  Server - DiscordMessenger:1
```

The above message will be shown if the token is either invalid OR it has expired.

<br/>

### Step 4 - Paste in your token

Carefully copy and paste your provided token over the string "some_invalid_token".. e.g

```lua
local myToken = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
```

Note, your token will be MUCH longer than the example above as it uses 256 bit encryption. You need to take care though that the token is properly pasted inbetween the two quotation marks!

<br/>

### Step 5 - Run the game again

Run the game again. This time, if your token is valid and has not expired you will see similar to:

```
Create discord client!  -  Server - DiscordMessenger:1
Discord responded with id 1144897406429823067 using author Spidey Bot on webhook id 1140580007635341404  -  Server - DiscordMessenger:1
```

Now take a look at Discord... you will see the message appear!

![Message received in Discord!](https://raw.githubusercontent.com/lowgold/rb-rologs-discord-message-sender/main/discord_message_received.png)