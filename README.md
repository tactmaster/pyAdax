# pyAdax

Python3 library for Adax heater. 

Control Adax heaters and get measured temperatures.

[Buy me a coffee :)](http://paypal.me/dahoiv)



## Install
```
pip3 install adax
```

## Example:

```python
from adax import Adax
import aiohttp
import asyncio

ACCOUNTID = "<ACCOUNT ID>"  # get your account ID (6 digits) from the Account page in the Adax WiFi app
PASSWORD = "<PASSWORD>" # create a service password under "Remote Api" in the app

async def main():
    async with aiohttp.ClientSession() as session:
        heater= Adax(ACCOUNTID, PASSWORD, session)
        for room in await heater.get_rooms():
            print(room)

asyncio.run(main())

```

Each room is a dict with, among others:

- `id`, `homeId`, `name`, `heatingEnabled`
- `temperature` and `targetTemperature` in C (`targetTemperature` is 0.0
  when heating is disabled)
- `energyWh`: the energy used so far in the current hour, summed over the
  room's heaters (only present if the room has a heater)
- `devices`: those heaters, each with `id`, `homeId`, `roomId`, `name`,
  `type`, `energyWh` and `energyTime` (when the energy was measured, in ms
  since the epoch)

