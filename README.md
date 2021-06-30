# ePaper-weatherDisplay
"Contacts a webserver for weather data (in JSON format) which it then displays on an ePaper display."

OK, that's the general idea. More specifically, it contacts my own weather server which records the weather outside my window. I'm using a BMP280 (which was bought as a BME280; the usual issue...), so I'm recording temperature and pressure, along with the battery voltage on the weather station, which is solar powered. The display looks like this:

![IMG_20210630_230434555_2](https://user-images.githubusercontent.com/5638741/124038180-a21f2900-d9f8-11eb-90cf-c1cfcc23b972.jpg)

There's quite a bit going on:
1) There's some legacy code I've left in for using a speaker, also for using an SD card; but neither are used in this sketch.
2) The first thing we actually do is get the WiFi going.
3) We then contact the Internet time server so we know what time it is (used later on).
4) If that goes to plan, we then contact my weather server and get a JSON response with my latest weather data in.
5) If that's all gone to plan, we then extract the weather data from the JSON feed and display it on the ePaper screen. 
6) The values are stored in the RTC memory (so it survives deep sleep), and next time, the new values are compared so that the display shows whether the new values are rising, falling, or staying steady.
7) We then work out how long to wait so that, next time, we awake about 5 minutes after the latest reading on my weather server (readings are once an hour).
8) Once we're in step, the display should wake up once an hour, update the weather values, then go back to sleep again.

Since we're sleeping for the most part of an hour, this seems a really good use of the ePaper display.

_David Argles, d.argles@gmx.com_
