# AI_Voice_News_Reader_Assistant 
Check it out: https://ai-voice-reader-assistant-anirban.netlify.app/
It's a complete Artificial Intelligent News Reader Voice Assistant

APIs used are:-
ALAN Ai, 
NewsAPI org

Script testing
After you have built a voice script, you need to make sure the conversation flow covers all usage scenarios, correct replies are given and the necessary actions are carried out when the user gives voice commands. Alan provides a set of tools to test voice scripts:

Debugging Chat
Test Mode view
Alan Studio logs
Debugging Chat
To the right of the code editor in Alan Studio, you can see the Debugging Chat. You can use this chat to test the script you are creating, either by giving voice commands or typing them.

To test a command with voice, in the Debugging Chat, click the Alan button and pronounce the command.
To test a command by typing it, in the text area of the Debugging Chat, type the command text and click the Send button or press ENTER on the keyboard.
test chat

In the Debugging Chat, commands and responses are displayed as bubbles. Every bubble is titled with the name of the voice script to which the command or response belongs and the number of the row in the voice script. To go to the corresponding code block in the code editor, click the link at the top of the bubble.

To let you quickly grasp how commands are built, the Debugging Chat displays slots in the user input as colored blocks. For example, if a command includes a slot and you say or enter the slot value, the Debugging Chat will display a block containing the slot value and name.

When you test a voice script in the Debugging Chat, you emulate the user interaction with your app. However, in some cases, giving commands may not be enough, and the Debugging Chat will fail to process commands in a proper way. This can happen, in particular, if the script requires some data from the app side.

To work around such issues, the Debugging Chat offers the following options:

Setting authentication data
Setting the visual state
Setting authentication data
If your application requires the user to authenticate to interact with it, you can set authentication data in the Debugging Chat. As a result, you will be able to run voice commands as if the user is logged in to the system.

To set authentication data, at the bottom left of the Debugging Chat, click the Set Auth Data button and enter the authentication data as JSON or a string, for example:

{
	"token": "demo", 
	"baseUrl": "https://mysite",
	"deviceId": "1234-5678-9001",
	"userName": "demo"	
}
Copy
Setting the visual state
The Set visual state option allows you to emulate the situation when your app passes some visual state to the script. As a result, commands that require the visual state will be processed as expected.

To set the visual state, at the bottom left of the Debugging Chat, click the Set Visual State button and enter the visual state as JSON. For example, if some commands in your script can be run only from specific app screens, you can specify the visual state in the following way:

{"screen": "Products"}
Copy
After that, you will be able to test all commands that require the {"screen": "Products"} visual state.

The Debugging Chat keeps the history of visual states set during the current session. Therefore, you can set several visual states and switch between them when needed.

Connecting from a mobile device
You can check how your voice script works using a mobile device. To do this, you need to connect to the script from the Alan Playground and give voice commands as if you are an app user. The given commands and replies will be sent to the Debugging Chat, and you will be able to review the results of voice commands execution in a convenient way.

To be able to test a voice script using a mobile device, you must have the Alan Playground installed on the device. For details, see Alan Playground.

To test how your script works using a mobile device:

At the bottom left of the Debugging Chat, click the QR code button. The QR code will be sent to the chat.
On your mobile device, open the Alan Playground.
Tap the Scan QR Code button and scan the QR code in the Debugging Chat with the device camera. The 'Mobile device connected' message will be sent to the Debugging Chat.
In the bottom right corner of your app on the mobile device, tap the Alan button and say voice commands.
qr code

Test Mode View
If you want to write tests for your script or even use the TDD methodology, you can switch to the Test Mode view in Alan Studio. Here you can plan and test different conversation flows for your project.

To test the voice script in the Test Mode view:

At the top right corner of the code editor, click Test Mode.
In the block in the center of the test area, enter the voice command you want to test. The command reply will be displayed in the section below.
Proceed to set up the whole conversation flow you want to test. You can create different conversation branches, several flows in one test case or add several test cases.
test mode

You can work with the prepared test flow in the following way:

To test all commands in the flow, at the top of the Test Mode view, click Run All.
To test a specific conversation flow, branch or command, hover over the necessary node in the flow and at the top right corner, click the play icon.
To duplicate a node, hover over it and at the top right corner, click the duplicate icon. The same node will be added at the same level in the flow.
To delete a node, hover over it and at the top right corner, click the delete icon.
If you need to save the test flow, you can export it. At the bottom left corner of the Test Mode view, click Import/Export, copy and save the text flow raw data. You can import it to any project in Alan Studio at any moment later.

How to make Alan use the plural form for nouns
To use the pluralizer in Alan, add the underscore character (_) to the necessary noun in the voice command.

This syntax is not supported for irregular plural nouns.

  intent("I want $(NUMBER) $(P cake_)", p => {
      p.play(`Here you are, ${p.NUMBER} ${p.P}`);
  })
  
How to use several slots of the same type in one intent
You can add a slot of the same type to one intent several times. In this case, all slot values will be collected in an array with the following name: SLOTNAME+s, for example, ITEMs.

For example, if you have several slots named ITEM, you can access the ITEMs object with an array of size 2 and you can reference the first item as ITEMs[0].

const items = ["burger", "cola", "taco"].join('|');
intent(`I want $(NUMBER) $(ITEM ${items}) and $(NUMBER) $(ITEM ${items})`, p => {
    let order = _.reduce(_.range(_.size(p.NUMBERs)), (acc, i) => {acc[p.ITEMs[i]] = p.NUMBERs[i].number; return acc}, {});
    p.play({command: "createOrder", order });
})
