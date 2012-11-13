###NAME:
    netyell - send formatted messages to symon netbrite signs

###INSTALL
	
Clone this repository or download it's contents. Run:

	chmod +x install.sh && install.sh

This requires that you have `pip` and `wget` installed on your system.
###SYNOPSIS:
    netyell "web\[{URL}<<{CSS-SELECTOR}[<<CSS-SELECTOR]*]+\{PYTHON-FORMAT-STRING}"
    [-b -d -e -f -l -r -s -v]
    netyell "{NETBRITE-SHORT-CODE-STRING}" [-b -d -e -f -l -r -s -v]
    netyell --help
    netyell --fonts
###FLAGS:
    --fonts		Returns a list of all available fonts and their short codes.
    -b		Prepends a blink tag to the message.
    -d		Runs netyell in debug mode, no http request will be sent.
    -e		Appends an erase tag to the message.
    -f		Parses the first argument as a url-selector string instead of the 
	        default (netbrite-shortcode string).
    -l[secs]	Loops the message, sending a recurring request every 5 seconds.
		    Or at whatever interval you specify.
    -r		Puts text in rainbow mode. WARNING: This greatly increases the size
      	    of the message which may cause the server to ignore it even though it
	        sends back a 200 status code.
    -s		Surrounds your message in wingbat symbols.
    -v		Returns verbose request output.
###EXAMPLES:
	1) Blinking text in rainbow mode.
	
	$ netyell "What is the speed air-speed velocity of an unladen swallow?" -b -r
	
	2) The serial of the sign in monospace 11, red, with surrounding wingbats. 
	
	$ netyell '&&f -> &&mo11:: !!r ^^s' -s
	
	3) The current weather and forecast for Seattle, WA.
	
	$ netyell 'web\http://www.weather.com/weather/right-now/47.606209,-122.332071?cm
	_ven=Googlemaps&cm_cat=googleOneBox&cm_pla=application-us&cm_ite=today<<[itempr
	op=temperature-fahrenheit]<<[itemprop=weather-phrase]<<[itemprop=observation-qu
	alifier-phrase]\&&f -> &&mo7:: Temp: %sF Weather: %s Forecast: %s' -f
	
	4) Get the titlei, points, and comment count of the top hackernews article every
	2 hours.
	
	$ netyell 'web\http://news.ycombinator.com/best<<td.title
	a<<[id^=score]<<[href^=item?]\!!rHN Top Article:!!y %s &&f ->
	&&mo7:: %s %s' -l7200 -f &
	       
###NETBRITE SHORT CODES:
    Netyell does not require you to use the full length netbrite tags. You can
    use these shortcuts:
     
		!!g: {green}
		::sof: {scrolloff}
		^^s: {serial}
		&&c: {center}
		::boff: {blinkoff}
		::son: {scrollon}
		&&r: {right}
		&&l: {left}
		::bon: {blinkon}
		::t ->: {tune 
		::b: {bell}
		!!r: {red}
		&&f ->: {font
		::p: {pause}
		!!y: {yellow}
		::e: {erase}
		:: : }