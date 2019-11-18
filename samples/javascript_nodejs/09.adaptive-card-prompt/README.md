# Adaptive Card Prompt Sample

Bot Framework v4 Adaptive Card Prompt Sample

// TODO: Update AdaptiveCardPrompt link once in SDK
This bot has been created using [Bot Framework](https://dev.botframework.com), it shows how to use the new [AdaptiveCardPrompt](https://github.com/mdrichardson/botbuilder-js/blob/adaptiveCardPrompt/libraries/botbuilder-dialogs/src/prompts/adaptiveCardPrompt.ts) to gather data in a dialog.

## AdaptiveCardPrompt Features

* Includes validation for specified required input fields
* Displays custom message if user replies via text and not card input
* Ensures input is only valid if it comes from the appropriate card (not one shown previous to prompt)

## Usage

```js
// Load an adaptive card
const cardJson = require('./adaptiveCard.json');
const card = CardFactory.adaptiveCard(cardJson);

// Configure settings - All optional
const promptSettings = {
    card: card,
    inputFailMessage: 'Please fill out the adaptive card',
    requiredInputIds: [
        'inputA',
        'inputB',
    ],
    missingRequiredInputsMessage: 'The following inputs are required',
    attemptsBeforeCardRedsiplayed: 5,
    promptId: 'myCustomId'
}

// Initialize the prompt
const adaptiveCardPrompt = new AdaptiveCardPrompt('adaptiveCardPrompt', null, promptSettings);

// Add the prompt to your dialogs
dialogSet.add(adaptiveCardPrompt);

// Call the prompt
return await stepContext.prompt('adaptiveCardPrompt');

// Use the result
const result = stepContext.result;
```

## Prerequisites

- [Node.js](https://nodejs.org) version 10.14 or higher

    ```bash
    # determine node version
    node --version
    ```

## To try this sample

- Clone the repository

    ```bash
    git clone https://github.com/Microsoft/botbuilder-samples.git
    ```

- In a terminal, navigate to `samples/javascript_nodejs/09.using-adaptive-cards`

    ```bash
    cd samples/javascript_nodejs/07.using-adaptive-cards
    ```

- Install modules

    ```bash
    npm install
    ```

- Start the bot

    ```bash
    npm start
    ```

## Testing the bot using Bot Framework Emulator

[Bot Framework Emulator](https://github.com/microsoft/botframework-emulator) is a desktop application that allows bot developers to test and debug their bots on localhost or running remotely through a tunnel.

- Install the Bot Framework Emulator version 4.3.0 or greater from [here](https://github.com/Microsoft/BotFramework-Emulator/releases)

### Connect to the bot using Bot Framework Emulator

- Launch Bot Framework Emulator
- File -> Open Bot
- Enter a Bot URL of `http://localhost:3978/api/messages`

## Adaptive Cards

Card authors describe their content as a simple JSON object. That content can then be rendered natively inside a host application, automatically adapting to the look and feel of the host. For example, Contoso Bot can author an Adaptive Card through the Bot Framework, and when delivered to Cortana, it will look and feel like a Cortana card. When that same payload is sent to Microsoft Teams, it will look and feel like Microsoft Teams. As more host apps start to support Adaptive Cards, that same payload will automatically light up inside these applications, yet still feel entirely native to the app. Users win because everything feels familiar. Host apps win because they control the user experience. Card authors win because their content gets broader reach without any additional work.

The Bot Framework provides support for Adaptive Cards.  See the following to learn more about Adaptive Cards.

- [Adaptive card](http://adaptivecards.io)
- [Send an Adaptive card](https://docs.microsoft.com/en-us/azure/bot-service/nodejs/bot-builder-nodejs-send-rich-cards?view=azure-bot-service-3.0&viewFallbackFrom=azure-bot-service-4.0#send-an-adaptive-card)

### Getting Input Data From Adaptive Cards

In a `TextPrompt`, the user response is returned in the `Activity.Text` property, which only accepts strings. Because Adaptive Cards can contain multiple inputs, the user response is sent as a JSON object in `Activity.Value`, like so:

```json
const activity = {
    [...]
    "value": {
        "inputA": "response A",
        "inputB": "response B",
        [...etc]
    }
}
```

Because of this, it can be a little difficult to gather user input using an Adaptive Card within a dialog. The `AdaptiveCardPrompt` allows you to do so easily and returns the JSON object user response in `stepContext.result`.

### Adding media to messages

A message exchange between user and bot can contain media attachments, such as cards, images, video, audio, and files.

## Deploy the bot to Azure

To learn more about deploying a bot to Azure, see [Deploy your bot to Azure](https://aka.ms/azuredeployment) for a complete list of deployment instructions.

## Further reading

- [Bot Framework Documentation](https://docs.botframework.com)
- [Bot Basics](https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0)
- [Adaptive Cards](https://adaptivecards.io/)
- [Send an Adaptive card](https://docs.microsoft.com/en-us/azure/bot-service/nodejs/bot-builder-nodejs-send-rich-cards?view=azure-bot-service-3.0&viewFallbackFrom=azure-bot-service-4.0#send-an-adaptive-card)
- [Activity processing](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-concept-activity-processing?view=azure-bot-service-4.0)
- [Azure Bot Service Introduction](https://docs.microsoft.com/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)
- [Azure Bot Service Documentation](https://docs.microsoft.com/azure/bot-service/?view=azure-bot-service-4.0)
- [Azure CLI](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
- [Azure Portal](https://portal.azure.com)