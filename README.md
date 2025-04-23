# Arduino-Switch...Case-on-strings

How to use switch...case on strings in Arduino IDE

If you have just a few ascii commands to handle, received by Serial, it's okay to use "If...Else If". But if you have many commands, with "If..Else If" you will lose overview easily.
In this case switch...case would be more convenient. Sadly Arduino IDE does't support switch with String objects. But with a trick it is possible.

1. First at all you must construct a "enum". enum is a kind of index array, starts at 0.
such like: 
enum Index { AB, BC, CD, DE, EF };

2. Then you must construct a String array with the same characters and sequences,
for example:
#define numberofCommands 5
const String Command[numberofCommands]={ "AB", "BC", "CD", "DE", "EF" };
The definitions are now finished.

3. In the Loop, the received string of Command commandString will be compared to the Command array first
whichCommand = 0;
while ((whichCommand <= numberofCommands) && (commandString != String(Command[whichCommand]))) {       // find command in array
	whichCommand++;
} 
Here is the trick: the increase of whichCommand stops at the position where the Command is found in Command array. And whichCommand has the same value as enum with the same characters.

4. Now we can use switch to handle all "Command", but in Index as alias of the Command array.
switch (whichCommand) {

   case AB:              
	break;

	case BC:              
	break;

	case CD:              
	break;

	case DE:              
	break;

	case EF:              
	break;

	default:              
	break;

}

