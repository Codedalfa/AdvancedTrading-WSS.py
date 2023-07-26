import asyncio
import os
import time
import hmac
import hashlib
import json
from dotenv import load_dotenv
from websockets import connect

# Load environment variables
load_dotenv()
API_KEY = os.getenv("API_KEY")
SIGNING_KEY = os.getenv("API_SECRET")


async def subscribe():
    async with connect('wss://advanced-trade-ws.coinbase.com') as websocket:
        timestamp = str(int(time.time()))

        # Define the request
        request = {
            "type": "subscribe",
            "product_ids": ["ETH-USD", "ETH-EUR"],  # Updated product IDs
            "channel": "heartbeats",
            "signature": "",
            "api_key": API_KEY,
            "timestamp": timestamp
        }

        # Generate the signature
        message = timestamp + 'heartbeats' + 'ETH-USD,ETH-EUR'
        signature = hmac.new(SIGNING_KEY.encode(
            'utf-8'), message.encode('utf-8'), digestmod=hashlib.sha256).digest()

        # Update the signature in the request
        request['signature'] = signature.hex()

        # Send the request
        await websocket.send(json.dumps(request))

        while True:
            response = await websocket.recv()
            print(f"< {response}")

asyncio.run(subscribe())
FooterCoinbase
Coinbase
