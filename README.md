<div align="center">

## ^ An  Image Verification Tutorial


</div>

### Description

Ever logged onto Yahoo! or here on Planet Source Code and have run across the verification image containing numbers and leters that you must plug into a form for verification? Learn to do it.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Darryl Porter](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/darryl-porter.md)
**Level**          |Beginner
**User Rating**    |4.8 (341 globes from 71 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Graphics/ Sound](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/graphics-sound__8-15.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/darryl-porter-an-image-verification-tutorial__8-739/archive/master.zip)





### Source Code

<br><br><br><big><b>Image Verification Tutorial</b></big><br><br>
<div align="center">
 <center>
 <table border="2" cellpadding="15" width="50%" style="border-collapse: collapse" bordercolor="#111111" cellspacing="0">
  <tr>
   <td width="100%" align="justify">I'm sure many of you have logged on to Yahoo!, eBay or even here on Planet
Source Code and have run across the verification image containing numbers and
letters that you must plug into an input box for verification. And maybe you
thought, &quot;What the heck is this for?&quot; or &quot;I wish I knew how to do that.&quot; <br>
You wanna know--then I will show you how.<br>
<br>
A script like this is usually used for further security of the user's
information--or, like on Planet Source Code, so that &quot;unscrupulous people&quot;
cannot use &quot;HTTP Post code in their submissions to trick people into unknowingly
voting for them.&quot;<br>
<br>
Okay, enough talk--let's get started.<br>
<br>
First, I assume that you have PHP 4 with the GD library already installed. Also,
   we will use session functions in this code to pass a varaible from one
   page to the next.<br>
<br>
To create our image, we need to send a header telling the connection that we are
about to send an image, we do that with the header function:<br>
--------------------------------------------<br>
<br>
<font color="#008000">&nbsp;/*Send header*/</font><br>Header(&quot;Content-Type: image/png&quot;);<br>
<br>
--------------------------------------------<br>
We are going to be working with png images in this tutorial. But if you want to
use &quot;jpeg&quot;, just plug it in where &quot;png&quot; is in the header. (You can also call a
&quot;gif&quot; image, but because of all the money stuff, most servers don't support it.)<br>
   <br>
   I know your dying to get started building images, but first, we need to
   get a little more prep work out the way. So, let's put those session
   functions to work. <br>
   ---------------------------------------------<br>
   <br>
   <font color="#008000">/* initialize a session. */</font><br>
   session_start();<br>
   <br>
   <font color="#008000">/*We'll set this variable later.*/</font><br>
   $new_string;<br>
   <br>
   <font color="#008000">/*register the session variable. */</font><br>
   session_register('new_string');<br>
   <br>
   -------------------------------------------------<br>
   All we did above was start a new session with the session start function.
   We will call this session on a different page that we will create later.
   Second, we created a variable called new_string that we will give a value
   to later. Lastly, we called the session register function: this function
   takes the variable we created as an argument minus the &quot;$&quot; sign, also, you
   must put it inside single quotes only. (An argument refers to the single
   or comma separated information inside the parenthesis of a function.)<br>
   <br>
With that out the way, we can now begin to create our image. We start this
   process by calling the create image function, which does
exactly what it says: Creates an image.<br>---------------------------------------------<br>
<br>
<font color="#008000">/* set up image*/<br>
/*The first number is the width and the second is the height*/</font><br>$im = ImageCreate(200, 40); &nbsp;<br>
<br>
----------------------------------------------<br>I set the image Create() function to the variable $im. The variable $im will be
our pointer to the image we just created for the rest of the tutorial. The image
Create function take only two arguments and the arguments can only be
integers (numbers). The first argument is the width of the image in pixels, the
second, you guessed it, is the height. <br>
<br>
Let's give our image some color.<br>----------------------------------------------<br>
<br>
<font color="#008000">/*creates two variable to store color*/</font><br>
$white = ImageColorAllocate($im, 255, 255, 255);<br>$black = ImageColorAllocate($im, 0, 0, 0);<br>
<br>
----------------------------------------------<br>
I called the Image Color Allocate function twice. The first time is to set the
color for white, the second to set the color for black. The function take 4
arguments: The image pointer variable $im, and the RGB (red, green, blue)
components that are separated by commas. <br>(255, 255, 255, is the code for white, while 0, 0, 0, is the code for black. You
can play with the numbers to produce any color you want.)<br>
At this point we have a png image and two colors. Now we will create a random
string generator to place as the verification code inside the image. I won't
discuss how the random generator code works, but will only lay out the code with
comments.<br>------------------------------------------------<br>
<br>
<font color="#008000">/*random string generator.*/<br>/*The seed for the random number*/</font><br>
srand((double)microtime()*1000000); <br>
<br>
<font color="#008000">/*Runs the string through the md5 function--which is a function that&nbsp;encrypts
a string, changing it into a 32 character string composed of numbers and
lowercase letters*/</font><br><br>
$string = md5(rand(0,9999)); <br>
<br>
/<font color="#008000">*Creates the new string. The first number is the point in
the 32 character string where we will pull our string from. In other words, PHP
will count (beginning at 0) 17 characters into the string. The 18th character in
will be our beginning point (remember, PHP starts counting from 0). From there,
PHP counts 5 characters from that point, and thus, we get our five character
string. The second number is the length of our string--changing this number will
give us different string lengths.*/</font><br>
$new_string = substr($string, 17, 5); <br>
-------------------------------------------------
<br>
<br>
Moving on--Now let's fill the image with color.<br>
-------------------------------------------------<br>
<br>
<font color="#008000">&nbsp;/*fill image with black*/</font><br>ImageFill($im, 0, 0, $black);<br>
<br>
---------------------------------------------------<br>
The Image Fill function is called first. It takes 4 arguments: Again we add the
image pointer variable $im, the second and third are<i> x, y</i> coordinates in
our image, 0, 0, being at the top left corner. Our image size is 200x40,
therefore, the bottom right corner would be 200, 40. The fourth argument tell
us with what color to fill the image with: In our case it is black.<br>
<br>
Now, let's add the string we just created to our image. <br>
----------------------------------------------------<br>
<br>
<font color="#008000">&nbsp;/*write string at coordinates (70,10) in the color white.
(70, 10) puts the string almost in the middle of the image.*/</font><br>
ImageString($im, 4, 70, 10, $new_string, $white);<br>
<br>
-----------------------------------------------------<br>
We have yet another function: Image String, and yes, it adds a string to our
image. It takes six arguments. The first is the image pointer variable, the
second argument can be any number from 1 to 5,(which calls for one of the built in fonts).
The next two arguments are the coordinates, first the x (width) then the y
(height). This is for the placement of our string. The next argument calls for the string
variable. In our case it is $new_string. The last argument is the variable containing the color, which is
$white.<br>
<br>
We end the image build by outputting our image using the code below:<br>
-----------------------------------------------------<br>
<br>
<font color="#008000">&nbsp;/*output to browser*/</font><br>ImagePNG($im, &quot;verify.png&quot;);<br>
ImageDestroy($im); <br>
<br>
------------------------------------------------------<br>
We have the imagePNG function with two arguments: again, like always the image
pointer, the second argument names the image &quot;verify.png&quot; and saves the
image in
the current directory. If you want the image in a different directory, proceed &quot;verify.png&quot;
with the path to the directory. <br>
<br>
Hey, we're through building the image. <br>
<br>
Finally,
input the Image Destroy function, it has one argument: the pointer variable.
Destroying the image frees up server memory. Your server administrator will like
you for this. Your code should look like this:<br>
-----------------------------------------------------<br>
<br>
&lt;?php<br>
   <font color="#008000">&nbsp;/*header*/</font><br>Header(&quot;Content-Type: image/png&quot;);<br>
   <font color="#008000"><br>
   /* initialize a session. */</font><br>
   session_start();<br>
   <br>
   <font color="#008000">/*We'll set this variable later.*/</font><br>
   $new_string;<br>
   <br>
   <font color="#008000">/*register the session variable. */</font><br>
   session_register('new_string');<br>
<font color="#008000"><br>
   /*You will need these two lines below.*/<br>
   </font>echo &quot;&lt;html&gt;&lt;head&gt;&lt;title&gt;Verification&lt;/title&gt;&lt;/head&gt;&quot;;<br>echo &quot;&lt;body&gt;&quot;;<p>
<font color="#008000">/* set up image, the first number is the width and the
second is the height*/</font><br>$im = ImageCreate(200, 40); <br>
<br><font color="#008000">/*creates two variables to store color*/</font><br>$white = ImageColorAllocate($im, 255, 255, 255);<br>$black = ImageColorAllocate($im, 0, 0, 0);<br>
<br><font color="#008000">/*random string generator.*/<br>/*The seed for the random number*/</font><br>
srand((double)microtime()*1000000); <br>
<br><font color="#008000">/*Runs the string through the md5 function*/</font><br>$string = md5(rand(0,9999)); <br>
<br>
<font color="#008000">/*creates the new string. */</font><br>$new_string = substr($string, 17, 5);<br>
<br>
<font color="#008000">&nbsp;/*fill image with black*/</font><br>ImageFill($im, 0, 0, $black);<br>
<br><font color="#008000">&nbsp;/*writes string */</font><br>ImageString($im, 4, 96, 19, $new_string, $white);<br>
<br>
<font color="#008000">/* output to browser*/</font><br>ImagePNG($im, &quot;verify.png&quot;);<br>
ImageDestroy($im); <br>
?&gt;<br>
---------------------------------------------------<br>
Now place a form input box below our image (see the code below), and ask the
user to input the string they see in the image in the text box. Append this code
to the bottom of the code above, before the &quot;?&gt;.&quot; <br>
---------------------------------------------------<br>
<br>
<font color="#008000">/*I plugged our image in like I would any other image.*/<br>
</font>echo &quot;&lt;img src=\&quot;verify.png\&quot;&gt;&quot;;<br>echo &quot;&lt;br&gt;&lt;br&gt;&quot;;<br>echo &quot;Type the code you see in the image in the box below. (case sensitive)&quot;;<br>
echo &quot; &lt;form action=\&quot;formhandler.php\&quot; method=post&gt;&quot;;<br>echo &quot;&lt;input name=\&quot;random\&quot; type=\&quot;text\&quot; value=\&quot;\&quot;&gt;&quot;;<br>echo &quot;&lt;input type=\&quot;submit\&quot;&gt;&quot;;<br>echo &quot;&lt;/form&gt;&quot;;<br>echo &quot;&lt;/body&gt;&quot;;<br>echo &quot;&lt;/html&gt;&quot;;<br>
<br>
   </p>
   <p>---------------------------------------------------<br>
   With that done, we must now create a new file and name it formhandler.php.
   We will put the code below into it.<br>
---------------------------------------------------<br>
   <br>
&lt;?php<br>
   <font color="#008000">/*This starts the session that we created on the
   last page*/</font><br>
   session_start(); <br>
   <br>
   <font color="#008000">/*This trims the random variable of any white space
   that the user may have unknowingly put in.*/</font><br>
   $random = trim($random);<br>
<font color="#008000"><br>
   /*Below is a conditional statement: In English it reads, if
the string that the user put into the text box is equal to what is in the image
then print to the screen, &quot;You are verified.&quot;&nbsp; If they are not equal it tells the
user to go back and try again.*/<br>
   </font><br>
   <font color="#008000">/*We can use the variable $new_string because we
   registered it into our session on the last page, it retains its value that
   it had on the first page.*/</font><br>
   if ($new_string == $random){<br>echo &quot;You are verified&quot;;<br>
}<br>
else{<br>echo &quot;Please go back and get verified.&quot;;<br>
}<br>?&gt;<br>
<br>
There you are. Try it out. IF you have any trouble send me an e-mail. And that's
that.<br>
   <br>
   Thanks to comments left below, this article has been updated by the
   Author.<br>
   <font size="1"><font size="3"><b>Please Rate this Tutorial!!!</b></font></font></p>
   <p>&nbsp;</td>
   </tr>
  </table>
 </center>
 </div>

