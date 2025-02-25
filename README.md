# Discord Bot with Python

![Discord Bot](./Assets/Discord%20Bot%20with%20Python.gif)

This repository contains the code for a Discord bot built using Python. The bot listens for the keyword `$meme` and responds with a random meme from Reddit.

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Running the Bot](#running-the-bot)
- [Code Breakdown](#code-breakdown)
- [Contributing](#contributing)
- [License](#license)

## Project Overview

This project demonstrates how to create a simple Discord bot using Python. The bot interacts with the Discord API to read and respond to messages in a Discord server. The primary feature of this bot is to fetch and display random memes from Reddit when the `$meme` command is issued.

## Features

- Responds to the `$meme` command with a random meme from Reddit.
- Logs in to the Discord server and stays online as long as the program is running.
- Easy setup and deployment using Python and the Discord API.


![How It Works](./Assets/How%20it%20works.png)

This section provides a visual representation of how the bot works. The bot listens for the `$meme` command, fetches a meme from the Meme API, and sends it back to the Discord channel.

## Prerequisites

Before you start, ensure you have the following:

- Python 3 installed.
- pip (Python package installer) installed.
- A Discord account.
- A Discord server with "Manager Server" permissions.

## Setup

1. **Install Python and pip**:
   - Ensure Python 3 and pip are installed on your system. You can download Python from [python.org](https://www.python.org/).

2. **Create a Discord Application**:
   - Go to the [Discord Developer Portal](https://discord.com/developers/applications).
   - Create a new application and add a bot.
   - Get the bot token and enable the "Message Content Intent."
   - Invite the bot to your Discord server using the URL generator.

3. **Install Required Packages**:
   - Install the `discord.py` and `requests` packages using pip:
     ```bash
     python3 -m pip install -U discord.py requests
     ```

## Running the Bot

1. **Clone the Repository**:
   - Clone this repository to your local machine:
     ```bash
     git clone https://github.com/mahfuzswe/Discord-Bot-with-Python.git
     ```

2. **Replace the Bot Token**:
   - Open the `bot.py` file and replace `'Your Token Here'` with your actual bot token.

3. **Run the Bot**:
   - Run the bot using the following command:
     ```bash
     python3 bot.py
     ```

4. **Test the Bot**:
   - In your Discord server, type `$meme` in any channel where the bot has permission to send messages. The bot should respond with a random meme.

## Code Breakdown

### `bot.py`

```python
import discord
import requests
import json

def get_meme():
    response = requests.get('https://meme-api.com/gimme')
    json_data = json.loads(response.text)
    return json_data['url']

class MyClient(discord.Client):
    async def on_ready(self):
        print('Logged on as {0}!'.format(self.user))

    async def on_message(self, message):
        if message.author == self.user:
            return
        if message.content.startswith('$meme'):
            await message.channel.send(get_meme())

intents = discord.Intents.default()
intents.message_content = True

client = MyClient(intents=intents)
client.run('Your Token Here')  # Replace with your own token
```

- **`get_meme` Function**: Fetches a random meme from the Meme API.
- **`MyClient` Class**: Extends `discord.Client` to handle events.
  - `on_ready`: Logs a message when the bot is successfully logged in.
  - `on_message`: Responds to messages starting with `$meme`.
- **Intents**: Sets the necessary permissions for the bot.
- **`client.run`**: Starts the bot with your token.

## Contributing

Contributions are welcome! If you have any suggestions or improvements, please feel free to open an issue or submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


