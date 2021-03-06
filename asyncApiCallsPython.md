### Asynchronous Network API Calls in Python 3.7
***
#### Context
A *synchronous* call is like ordering a latte at the coffee bar, then waiting there for the cashier to make your latte. No other barista can help. You stand at the bar until the cashier makes the latte. The next customer can order when your latte has been given to you.

An *asynchronous* call is like ordering a latte at the coffee bar, then sitting down at a table and reading your book. The cashier hands your order off to a barista and helps the next customer. When the barista makes your latte, you go and retrieve it. Enjoy.

The same concepts apply to network API calls. Synchronous calls wait and block the process until the desired information is retrieved. Asynchronous calls assign functionality to a separate process, with the desired information retrieved and returned to the original process. 

Both calls *wait*, but the difference is whether or not the calls block. Synchronous calls block. Asynchronous calls do not.

This document describes a simple asynchronous approach for retrieving and displaying weather information. You will use the [OpenWeatherMap API](https://openweathermap.org) to retrieve the current temperature for a given US zipcode.

For further discussion on asynchronous and synchronous programming, refer to [this Mozilla article](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts).

#### Example Python 3.7 Code
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
#### Output
```
Temperature in Fahrenheit: 64.13
```

#### Implementation Details
Your `get_temperature()` function does the following:
1. Calls the remote weather API.
2. Waits for a JSON response.
3. Parses the response.
4. Prints the current temperature in the console.

All of this functionality runs asynchronously via `asyncio.run()`. 

In Python 3.7, the `asyncio` module provides `asyncio.run()`. At the top of the Python file, import `asyncio` and the other two required modules.

```python
import aiohttp
import asyncio
import json
```

Next, define `get_temperature()`. The `async` keyword tells Python that the function will wait asynchronously for an API response. 

```python
async def get_temperature():
``` 

After defining common variables (`base_url` and `endpoint`), create a [Client Session](https://docs.aiohttp.org/en/stable/client_reference.html) and assign it to a variable called `session`.

```python
async with aiohttp.ClientSession() as session:
```

Then call `get()` and assign the result to a variable called `response`. Consult the [OpenWeatherMap API](https://openweathermap.org/current#one) for information on the endpoint's parameters and possible values.

```python
async with session.get(base_url + endpoint +
                       'zip=94134&'
                       'units=imperial&'
                       'appid={APP KEY}') as response:
```

Specifying a function as `async` requires a subsequent `await`. In this case, you `await` the text result of `response`.

```python
network_response = await response.text()
```

The `json.loads()` function converts your JSON response to a dictionary. Subscript the dictionary to obtain the temperature, then `print()` the result.

```python
json_dictionary = json.loads(network_response)
print('Temperature in Fahrenheit: ' + str(json_dictionary['main']['temp']))
```

Finally, run the program and verify the results. 

```python
python asyncApiCallsPython.py
```
