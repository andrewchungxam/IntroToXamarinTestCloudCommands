# Intro to Xamarin Test Cloud Commands

This guide is an introduction the commands you will use and see with Xamarin Test Cloud.
The framework we will be exploring is called UITest -- written in the language of C#

You will see these commands in both Xamarin Test Recorder and in the REPL

This guide is meant as an explaination at first but also a cheat sheet that you can refer back to.
We will discuss the most commonly used commands.

COMMON COMMANDS - CHEAT SHEET:
<li>app.Tap("button1"); 
<li>app.EnterText (x => x.Id ("edit_phone"), "5555555555");</li>
<li>app.PressEnter();
<li>app.DismissKeyboard ();</li>
<li>app.WaitForElement("button2");
<li>app.Screenshot ("User enters phone number");</li>
</ul>                                                                    
<br />  
 
DEFINITION OF COMMON COMMANDS:

Definitions of the Commands Seen in Test Recorder:
1. app.Tap("button1"); 
* app.Tap("button1") is the most common guesture you'll use.  It mimics a user's tap on the app.  The "button1" represent a button marked with a "button1" id or label.
2. app.EnterText (x => x.Id ("edit_phone"), "Type this");</li>
* Use this command to enter text.  In the above command - the keyboard will type out "Type this" into a UIElement with the ID "edit_phone"
3. app.PressEnter();
* this is one way to submit the text you typed with EnterText - however, in some cases, you may want to dismiss the keyboard and press a Submit button 
4. app.DismissKeyboard();
* this is how you dismiss your keyboard after you enter text
5. app.WaitForElement("button2")
* this is how you get your test to wait for a particular element for up to 90 seconds.  This is really important when your app needs to do a lot of web requests or if the app takes some time to process your requests.  Rather than failing if the element doesn't appear right away, it will wait up to 90 seconds for the element to appear.  This is important when doing your local tests but even more important when you're doing your tests on the Xamarin Test Cloud.
6. app.Screenshot("User enters phone number")
* this is how you tell your application to take a screenshot -- in the Xamarin Test Cloud UI, each step will be denoted by the text you write in this method.  In the above case, it will be "User enters phone number" -- and the Xamarin Test Cloud web page will show a screenshot of your application.

---------------------------

# Understanding the syntax of the commands

In the cheat sheet - you've seen this command or commands similar to it:
* app.Tap("button1"); 

However, when you look at the code generated by Xamarin Test Recorder - you'll likely see that this code written like this:
* app.Tap(x=>x.Marked("button1"));

Both commands will do exactly the same thing!  However, the second command is the long-hand way to fully write out the command.  
<br/>
In both cases, the command is looking for any UI elements with an "Id", "label", or "text" that is reads exactly "button1".  Id is how items are referenced in iOS and lable is how things are referenced in Android.  Both iOS and Android will reference Text for the displayed Text.

In general - you should prefer to link your tests to an "Id" or a "label" over "text" - the reason is that the "text" can easily change as the marketing or business requirements or even language requirements can necessitate frequent changing of the text.

For more about the general C# syntax of this => notation - take a look at this [post](http://stackoverflow.com/questions/274022/how-do-i-pronounce-as-used-in-lambda-expressions-in-net).

---------------------------
# Why do I so often see x=>x.Class("something") and why do I sometime even see a .Index(3) after it?

When you look at the commands that Test Recorder gives back to you -- it will often show up as app.Tap(x=>x.Marked("button1")).  This is the most straightforward output type that you'll see in Test Recorder.

However, sometimes the commands cannot be simplied into the above "straightforward" style.  This is the case when the Id or label fields are not clearly marked.  

``` :star: Why would Id/label not be clearly marked?  It is actually up to the developer of the iOS or Android application itself, who can set the Id or label of the different controls when they are developing the app.  Setting the Id/label increases the robustness and simplicity of the tests and so we advocated a close collaboration between QA and your application developers.) :star: ```

So in the case when the Id or label fields are not clear -- then Test Recorder will start chaining Classes and Indexes so you'll see something like this:
app.Tap(x=>x.Class("UITextField").Index(0));

So to translate that; it is looking through all of the elements of the UI, and then making a list of all the elements with Class("UITextField") and then in that list, it is finding the element marked Index(0).

---------
What do you mean by Class?



---------
What is Index(0)?  
Simply put Index(0) is the first element in the group of elements.

So in this group of elements:
''[0 55 33 22 44]''

Index(0) of the above would be 0.  Index(1) would be 55.  Index(2) would be 33.

So to recap - would you see something like this:
app.Tap(x=>x.Class("UIView").Index(23));

It is looking for 



CLASS / INDEX(0) / what happens when the thing you get references something that shows up more than "once"


<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

<ul>Definitions of the Commands Seen in Test Recorder:
<li>app.Tap("button1"); 
* app.Tap("button1") is the most common guesture you'll use.  It mimics a user's tap on the app.  The "button1" represent a button marked with a "button1" id or label.
<li>app.DismissKeyboard ();</li>
<li>app.EnterText (x => x.Id ("edit_phone"), "5555555555");</li>
<li>app.PressEnter();
<li>app.ScrollUp ("CREATE", "linear_item");</li>
<li>app.ScrollDown ("CREATE", "linear_item");</li>
<li>app.ScrollDownTo ("CREATE", "linear_item");</li>
<li>app.Screenshot ("User enters phone number");</li>
<li>app.WaitForElement("button2");
</ul>



----
<ul>Common Notations and Terms seen in Test Recorder:
<li>app.Tap(x=>x.Marked("hello_button"));
<li>app.Tap(x=>x.Class("UIButton"));</li>
<li>app.Tap(x=>x.Id("hello_button"));</li>
<li>app.Tap(x=>x.Label("hello_button"));</li>
<li>app.Tap(x=>x.Text("Hello there!"));</li>
</ul>
----
<ul>Common repl commands:
<li>tree</li>
<li>app.Flash("myButton");</li>
<li>app.Flash(x=>x.All("*"));</li>
<li>app.Flash(x => x.All("*").Class("UITextFieldLabel").Text("User ID"));</li>
<li>app.TapCoordinates(153, 86);</li>
<li>app.Repl ();</li>
<li>copy
</ul>
----
<ul>
Common UI commands:
<li>app.DismissKeyboard ();</li>
<li>app.Screenshot ("User enters phone number");</li>
<li>app.EnterText (x => x.Id ("edit_phone"), "5555555555");</li>
<li>app.ScrollDownTo ("CREATE", "linear_item");</li>
<li>app.SwipeRightToLeft (c => c.Id ("txt_title"));</li>
<li>app.DragCoordinates (200, 400, 200, 800); // (from X, from Y, to X, to Y)</li>
<li>app.Query(x=>x.Class("FormsTextView").Index(0)) </li>
</ul>
<ul>
