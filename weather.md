### Asynchronous Network API Calls in Python
***
Asynchronous programming is like ordering coffee at the cash register, then sitting down and reading a book. The cashier helps the next customer while another barista makes your coffee. When your number is called, you go and retrieve your coffee.

In contrast, synchronous programming is like ordering coffee at the cash register and then waiting there for the cashier to make your coffee. You stand there until the coffee is done.

As an example API, we'll use the [OpenWeatherMap API](https://openweathermap.org) to asynchronously retrieve the current temperature.

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
