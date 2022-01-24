from unicodedata import name
from requests import Request, Session
from requests.exceptions import ConnectionError, Timeout, TooManyRedirects
import json
import pprint
import schedule
import time
import os
from twilio.rest import Client
#confirm all listed libraries have been installed before running script

account_sid = "{INSERT ACCOUNT SID}"
auth_token = "{INSERT ACCOUNT TOKEN}"

client = Client(account_sid, auth_token)

#Using Coin Market Cap API but can change to another API if desired. This example tracks the THOR Token 
def coin_track():
    url = 'https://pro-api.coinmarketcap.com/v1/cryptocurrency/quotes/latest'
    parameters = {
      'slug': 'thor',
      'convert':'USD'
    }
    headers = {
      'Accepts': 'application/json',
      'X-CMC_PRO_API_KEY': '{INSERT ACCOUNT KEY}',
    }

    session = Session()
    session.headers.update(headers)

 #Information prints in JSON format, with specific variables being stored in nested dictionaries.
 #We access these variables by digging through the layers of the dict
    response = session.get(url, params=parameters)
    data = json.loads(response.text)
    name = pprint.pprint(data['data']['15789']['name'])
    prices = int((data['data']['15789']['quote']['USD']['price']))
    print(prices)

 #Store values in variable list to perform further analysis and potential Machine Learning Implementation
    tracking = list()
    tracking.append(prices) 

    for i in range(len(tracking)):
      # Insert desired condition to trigger text message 
      if tracking[i] > 190:
        client.messages.create(
        to = "(Insert your phone number)",
        from_=  "(Insert Twilio phone number)",
        body = "(Insert text to be displayed in message)"
)

# This can be changed to trigger the function to run at whatever frequency you desire
schedule.every(10).seconds.do(coin_track)
while 1:
    schedule.run_pending()

