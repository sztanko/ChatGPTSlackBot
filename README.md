# revChatGPT

This is a simple Slackbot that uses the `revChatGPT` package to respond to messages in Slack. It is designed to be used with the Slack Events API, and it listens for `app_mention` events, which are triggered when a user mentions the bot in a Slack channel.

When the bot receives a `app_mention` event, it extracts the user's message from the event payload, sends it to the `revChatGPT` package to generate a response, and then sends the response back to the user via Slack.

The `revChatGPT` package is used to handle authentication and communication with the GPT-3 API, and it is also used to refresh the session with the GPT-3 API on a regular basis. This is done in a separate thread to prevent the session from expiring while the bot is handling requests.

## Usage

To use the bot, you will need to install the dependencies and set the `CHATGPT_EMAIL` and `CHATGPT_PASSWORD` environment variables with your OpenAI credentials. You can then run the `main.py` script to start the bot.

```python
pip install -r requirements.txt
export CHATGPT_EMAIL=your_openai_email
export CHATGPT_PASSWORD=your_openai_password
python main.py
```

Once the bot is running, you can mention it in a Slack channel to send it a message. For example, you can type `@my-bot hello` to send the message "hello" to the bot. The bot will respond with a generated message based on the GPT-3 model.

## Configuration

The `ChatGPTConfig` dictionary at the top of the `main.py` script contains the configuration for the `revChatGPT` package. It specifies the email and password for the OpenAI account that the bot will use to authenticate with the GPT-3 API. These values are read from the `CHATGPT_EMAIL` and `CHATGPT_PASSWORD` environment variables.

The `conversation_id` parameter in the `Chatbot` constructor is used to specify the ID of the conversation that the bot should use. If this parameter is not provided, the `revChatGPT` package will generate a new conversation ID for each message that the bot receives.

## Limitations

The bot uses a pre-trained GPT-3 model, which means that its responses are limited to the information that is contained in the model. It may not be able to respond accurately to messages that are outside of the scope of the pre-trained model.

Additionally, the bot is only designed to handle `app_mention` events, so it will not respond to other types of messages. This can be easily extended by adding more event handlers to the `main.py` script.

## Notes

The `tls-client` python library that is used by the `revChatGPT` package does not currently support ARM architectures. As a result, the bot may not be able to run on devices with ARM processors. This limitation will be addressed in a future update.
