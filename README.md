Previously, this wasn't possible.

But in 2020, Discord introduced two new features: Slash Commands and Interactions Endpoints.

Here's a very straightforward guide to getting you started.

<br>

<p align="center">
  <img src="https://discord.com/assets/a660b11b63a95e932719346ff67ea60f.png" alt="Slash Commands"></img>
</p>

<h6 align="center"><i>(This is what Slash Commands look like)</i></h6>

<br>

### 1. Setting up the Bot and the First Command

If you don't have one already, go to [Discord's Developer Portal](https://discord.com/developers/applications) and create a new app.

And, make sure to go to `Settings` and `Bot` and setup the Bot user. because you will need the bot `TOKEN`.

Now, you need to register new application command to test the bot.
This is currently only possible via HTTP endpoint.

```python
# global commands are cached and only update every hour
# url = f'https://discord.com/api/v8/applications/{APP_ID}/commands'

# while guild commands update instantly
# they're much better for testing
url = f'https://discord.com/api/v8/applications/{APP_ID}/guilds/{GUILD_ID}/commands'

json = {
  'name': 'bleb',
  'description': 'Test command.',
  'options': []
}

response = requests.post(url, headers={
  'Authorization': f'Bot {BOT_TOKEN}'
}, json=json)

print(response.json())
```


<h6 align="center"><i>(This is a script you keep to yourself and run locally each time you want to create/update your application's commands)</i></h6>

<br>

Your `App ID` is visible through **General Information** in your app dev portal.

To get a `Guild ID`, go to your discord client and enable **Developer Mode** in the **Advanced** Settings,
then go to the server and right-click on the sever's name in the top-left. And now should see a new entry in the context menu called **Copy ID**.

`Bot Token` is also visible through **Bot** in the app dev portal.

If you are creating if you are using guild commands *(You should for testing commands and for private bots)*.
Then before running the script you need to go to **OAuth2** then **OAuth2 URL Generator**. Click `applications.commands` and go to the generated URL to authorize the app.
Select the server you just copied the ID of, or the script won't work.


You should be able now to go the the server type `/` in the chat and see the command you' created, if not then something is wrong, try again until you can.


### 2. The AWS Lambda Function


