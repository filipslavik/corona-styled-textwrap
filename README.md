corona-styled-textwrap
======================

A pure-Lua text rendering module for Corona SDK which can handle basic HTML, fonts, and even basic font metrics.

I've made this library public in the hopes that we can fix the bugs and improve it. The documentation is poor, I know...feel free to help, or ask me questions!!!

It has a major flaw right now -- it cannot render styled text that is right/center justified. So sad. Hard to fix.

However, for everything else, it is fantastic. I use it for my ebook app, and it is fast and flexible.

<pre>
local params = {
  text = mytext,
	font = "AvenirNext-Regular",
	size = "12",
	lineHeight = "16",
	color = {0, 0, 0, 255},
	width = w,
	alignment = "Left",
	opacity = "100%",
	minCharCount = 5,	-- 	Minimum number of characters per line. Start low.
	targetDeviceScreenSize = screenW..","..screenH,	-- Target screen size, may be different from current screen size
	letterspacing = 0,
	maxHeight = screenH - 50,
	minWordLen = 2,
	textstyles = textStyles,
	defaultStyle = "Normal",
	cacheDir = cacheDir,
	handler = handler,  -- a function that will accept a 'tap' event
	hyperlinkFillColor = hyperlinkFillColor, -- an RGBa color in a string, like this: "200,120,255,100"

}
local t = textwrap.autoWrappedText(params)
</pre>

<b>Notes on the hyperlinking:</b>

<b>handler</b> : a function that will use a 'tap' event. Note that event.target._attr contains the attributes 
the hyperlink, e.g. href, style, class, whatever your throw in. 
In the example, the function will get 'makeSound' as the href, and it can do the appropriate action. 
You can pass any attribute you need, such as a page number or URL, of course.<br>
Example: &lt;a href="makeSound" style="font-size:24;"&gt;My Link&lt;/a&gt;

<b>Understanding the parts:</b>
- textwrap.lua : the module that renders a piece of text. The text can have basic HTML coding (p, br, i, em, b, li, ol), as well as my built-in paragraph formatting. It will also read the 'class' attribute of HTML to figure out the style, then apply the style from the textstyles.txt file!
- HTML support: entities.lua, html.lua : these are open source modules I found and modified to handle HTML
- fontmetrics.lua, fontmetrics.txt, fontvariations.txt : this module and files let the textwrap module position type correctly on the screen. Normally, you can't position with baseline, but these modules let us do that.
- funx.lua : a large collection of useful functions
