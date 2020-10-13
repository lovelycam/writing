### Sample: Asynchronous API Calls in Python
###### Chris Campbell
***

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
