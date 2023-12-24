```
import asyncio
import json
import websockets
import random
from randcrack import RandCrack
rc = RandCrack()
N = 1_000_000

async def send_json_to_websocket(json_data, websocket_url):
    headers = {'User-Agent': 'Mozilla/5.0'}  # You can adjust or add headers as needed
    
    try:
        async with websockets.connect(websocket_url + "/ws", extra_headers=headers) as websocket:
            for i in range(800):
                # Convert the JSON data to a string
                
                json_str = json.dumps(json_data)
                
                # Send the JSON string to the WebSocket
                await websocket.send(json_str)
                print(f"Sent JSON data to {websocket_url}: {json_str}")
                
                response = await websocket.recv()
                print(f'Received response from {websocket_url}: {response}')

                # Extract guess_id from the response
                response_data = json.loads(response)
                guess_id = response_data.get("guess_id")
                print(i)
                if i < 624:
                    rc.submit(guess_id)
                
                if i > 622:
                    num1 = rc.predict_getrandbits(32)
                    num2 = (num1 % N) +1
                    print("Predicted" , num2)
                else:
                    num2 = 1
                    # Create new JSON data with the updated "number" value
                json_data = {
                    "type": "guess",
                    "number": num2
                }

    except websockets.exceptions.InvalidStatusCode as e:
        print(f"Failed to connect to {websocket_url}. Status code: {e.status_code}")

# Initialize RandCrack instance
rc = RandCrack()

# Initial JSON data to be sent
json_data = {
    "type": "guess",
    "number": 1
}
websocket_url = "ws://chal1.gryphons.sg:8005"
asyncio.run(send_json_to_websocket(json_data,websocket_url))
```
Predicted 576037
Sent JSON data to ws://chal1.gryphons.sg:8005: {"type": "guess", "number": 576037}
Received response from ws://chal1.gryphons.sg:8005: {"flag": "GCTF23{p$eUDoR4ndOM_iS_N07_trUe_Random}", "type": "flag"}
798
