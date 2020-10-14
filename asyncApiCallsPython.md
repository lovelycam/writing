### Asynchronous Network API Calls in Python 3.7
***
##### Context
A synchronous call is like ordering a latte at the coffee bar, then waiting there for the cashier to make your latte. There's no other barista available to help. You stand there until the latte is made. The next customer isn't helped until your latte has been given to you.

An asynchronous call is like ordering a latte at the coffee bar, then sitting down at a table and reading your book. The cashier hands your order off to a barista and helps the next customer. When the barista makes your latte, you go and retrieve it. Enjoy.

The same concepts apply to network API calls. Synchronous calls wait and block the main process until the desired information is retrieved. Asynchronous calls assign functionality to a separate process. The desired information is retrieved in this separate process and then returned to the main process. 

Both approaches "wait", but the difference is whether or not this waiting blocks the main process. Synchronous calls block. Asynchronous calls do not.

This document describes a simple asynchronous approach for retrieving and displaying weather information. We'll use the [OpenWeatherMap API](https://openweathermap.org) to retrieve the current temperature for a given US zipcode.

For further discussion on asynchronous and synchronous programming, refer to [this Mozilla article](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts).

##### Example Python 3.7 Code
```python
import aiohttp
import asyncio
import json

async def get_temperature():
    base_url = 'https://api.openweathermap.org/data/2.5/'
    endpoint = 'weather?'

    async with aiohttp.ClientSession() as session:
        async with session.get(base_url + endpoint +
                               'zip=94134&'
                               'units=imperial&'
                               'appid={APP KEY}') as response:
            network_response = await response.text()
            json_dictionary = json.loads(network_response)
            print('Temperature in Fahrenheit: ' + str(json_dictionary['main']['temp']))

asyncio.run(get_temperature())
```
##### Output
```
Temperature in Fahrenheit: 64.13
```

##### Implementation Details
What does the above code do? Basically, the `get_temperature()` function calls the remote weather API, waits for a JSON response, parses this response, and then prints a temperature in the console. All of this functionality runs asynchronously via `asyncio.run()`. 

In Python 3.7, `asyncio.run()` is provided in the `asyncio` module. We import `asyncio`, as well as the other two required modules, at the top of the Python file.

```python
import aiohttp
import asyncio
import json
```
We then implement `get_temperature()`. Notice the `async` keyword in the function definition. This tells Python that the function will wait asynchronously for an API response. 

```python
async def get_temperature():
``` 

