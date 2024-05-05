import os
import requests
import discord
import time
intents = discord.Intents.default()
intents.message_content = True

client = discord.Client(intents=intents)


def fetch_hypixel_status(uuid):
  url = "https://api.hypixel.net/status?key=b6f72fcd-7de6-4ab0-bfa1-f995a3cc128b&uuid=" + uuid

  try:
      response = requests.get(url)
      data = response.json()

      if 'session' in data and 'online' in data['session']:
          if data['session']['online']:
              player_status = f"{data['session']['gameType']} - {data['session']['mode']}"
              #return f"The player is currently online playing {player_status}."
              return "online"
          else:
              return "The player is currently offline."
      else:
          return "Unable to fetch player status." + str(data)
  except Exception as e:
      return f"An error occurred: {str(e)}"


def send_message_through_webhook(webhook_url, message):
  data = {
      "content": message
  }

  try:
      response = requests.post(webhook_url, json=data)
      response.raise_for_status()
      print("Message sent successfully!")
  except requests.exceptions.HTTPError as err:
      print(f"HTTP error occurred: {err}")
  except Exception as e:
      print(f"An error occurred: {e}")
webhook_url = "https://discord.com/api/webhooks/1220578767517515916/IVOGNswR7JsFgkbVQD7lU-_VHlYS2CyLTEEzY-uFgC-oxeYEXlgEeJ4t4IvmMtMQgV5w"
#message = fetch_hypixel_status("b8f62842-1931-4431-8636-0332ade7a6fb")

# Call the function to send the message
#send_message_through_webhook(webhook_url, message)

users = [["7f94e1e5-9001-4323-84a6-f22e6611207a",0,"Karmalord21"],["b8f62842-1931-4431-8636-0332ade7a6fb",0,"NetherRiley"],["f342d588-de6e-416b-b0e4-da8e1d1e8056",0,"plspareme"],["d47a0501-51fd-44d9-8e2d-afdf60177904",0,"CreatorofBob1"],["8affd1db-d5af-45c1-88a1-75e579ab5a6b",0,"plsaveme"]]
karmalord = False
netherriley = False
plspareme = False
creatorofbob = False
while True:
    for i in users:
        if fetch_hypixel_status(i[0]) == "The player is currently offline." and i[1] == 1:
            send_message_through_webhook(webhook_url,i[2] + " hopped off!")
            i[1] = 0
        elif fetch_hypixel_status(i[0]) == "online" and i[1] == 0:
            send_message_through_webhook(webhook_url,i[2] + " hopped on!")
            i[1] = 1
        print(fetch_hypixel_status(i[0]))
    time.sleep(10)
    print(users)
