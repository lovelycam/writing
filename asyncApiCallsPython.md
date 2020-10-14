### Asynchronous Network API Calls in Python
***
##### Context

An *asynchronous* call is like ordering a latte at the coffee bar, then sitting down at a table and reading your book. The cashier hands your order off to a barista and helps the next customer. When the barista makes your latte, you go and retrieve it. Enjoy.

In contrast, a *synchronous* call is like ordering a latte at the coffee bar and then waiting there for the cashier to make your latte. There's no other barista available to help. You stand there until the latte is made. The next customer isn't helped until your latte has been given to you.

The takeaway is whether or not there's more than one barista available. If there is, the making of the latte can be handed off, while the cashier can continue taking customer orders. However, if there's only one barista, you and everyone behind you in line has to wait for the barista to finish.

In technical terms, asynchronous calls hand off functionality to a background process, so as not to "block" further execution in the main process. The desired information is retrieved in the background then returned to the main process. In contrast, synchronous calls wait and block the main process until the desired information is retrieved.

For further discussion on asynchronous and synchronous programming concepts, refer to [this Mozilla article](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts) 

This document describes a simple asynchronous approach, in Python, for retrieving and displaying weather information. We'll use the [OpenWeatherMap API](https://openweathermap.org) to retrieve the current temperature for a given US zipcode.

##### Example Python 3 Code
```python
import aiohttp
import asyncio
import json

async def main():
    base_url = 'https://api.openweathermap.org/data/2.5/'
    endpoint = 'weather?'
    
    async with aiohttp.ClientSession() as session:
        async with session.get(base_url + endpoint + 'zip=90210&'
                                                     'units=imperial&'
                                                     'appid={APP KEY}') as response:
            json_response = await response.text()
            json_dictionary = json.loads(json_response)
            print('Temperature in Fahrenheit: ' + str(json_dictionary['main']['temp']))

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```
##### Output
```
Temperature in Fahrenheit: 64.13
```

##### Implementation Details

