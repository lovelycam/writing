### Asynchronous Network API Calls in Python
***
##### Context

An *asynchronous* call is like ordering a latte at the coffee bar, then sitting down at a table and reading a book. The cashier helps the next customer while a barista makes your latte. When your number is called, you go and retrieve your latte.

In contrast, a *synchronous* call is like ordering a latte at the coffee bar and then waiting there for the cashier to make your latte. You stand there until the latte is done. There is no other barista available to help.

The key takeaway is whether or not there is more than one barista available to make your latte. If there's only one barista, then you and everyone behind you in line has to wait for the barista to finish. If there is more than one barista, the making of the latte can be handed off, while customer orders can continue to be taken.

In technical terms, asynchronous calls hand off functionality to a background process, so as not to "block" further execution in the main process. Synchronous calls wait and block the main process until the desired information is retrieved.

This document describes a simple asynchronous strategy for retrieving and displaying weather information.

As an example API, we'll use the [OpenWeatherMap API](https://openweathermap.org) to asynchronously retrieve the current temperature for a given US zipcode.

##### Example Python Code
```python
import aiohttp
import asyncio
import json

async def main():
    base_url = 'https://api.openweathermap.org/data/2.5/'
    endpoint = 'weather?'
    
    async with aiohttp.ClientSession() as session:
        async with session.get(base_url + endpoint + 'zip=94134&'
                                                     'units=imperial&'
                                                     'appid={APP KEY}') as response:
            json_response = await response.text()
            json_dictionary = json.loads(json_response)
            print(json_dictionary['main']['temp'])

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
```
