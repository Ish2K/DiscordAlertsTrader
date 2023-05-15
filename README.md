# DiscordAlertsTrader: *Discord Alerts Trader Bot*
________________________

DiscordAlertsTrader is a python package to get messages from a subscribed discord channel where buy
 and sell stock and options signals are messaged. The package will parse the messages and execute
 the trades for traders specified in the config file. It will track the messages from all channels,
 the analysts portfolio and the bot portfolio.

If no brokerage API key is provided, it will just print the discord messages and track the analysts
 portfolio. With a TDA API key, it will track current price of the alerts, and calculated PnL-current.

If in config.ini DO_BTO_TRADES = false, not trades will be executed. 

Trades are done through TDAmeritrade API, implementing webull and etrade.  

What this package does:

- Read messages and parse trading singals, e.g. BTO (Buy to Open), STC (Sell to Close), partial STC, SL (Stop Limits), PT (Profit Taking)
- Track trading signals and performance of traders using message history and realtime price
- Execute and cancel orders, check order status, account status and current ticker prices

control trade execution manually, through promts choose QTY, price, etc

**Currently, the package is for parsing signals of the discord server BullTrades.** 

Invite link to BullTrades: https://discord.gg/bulltrades


 ## Discord user token
 ______________________________

It requires a user discord token, then change config_example.py to config.py. There needs to be:

Discord token to access discord message chats:
```
discord_token = "token0Y03e..."
```
to get discord token and channels IDs follow the instructions in: https://github.com/Tyrrrz/DiscordChatExporter/blob/master/.docs/Token-and-IDs.md

Channel ID of the channel were trading alers are messaged (left click on channel and go to channel ID):
```
channel_IDS = {"stock_alerts": 6666,
               "option_alerts": 4444,
               "options_chat": 5555}
```





## Setup and Run
______

First of all **install python**. For windows you can run this in the PowerShell, if you see the output print "Hellow, World!" python with conda is installed:
```# Check if Scoop is installed
if (-not (Test-Path $env:USERPROFILE\scoop)) {
    # Install Scoop
    Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
    irm get.scoop.sh | iex
}
scoop install git
# Check if extras are included
$extras = scoop bucket list | Select-String -Pattern '^extras$'
if (-not $extras) {
    # Add the extras bucket    
    scoop bucket add extras
}

# Install Miniconda3
scoop install miniconda3

# Run Python script
python -c "print('Hello, World!')"
```

then in the terminal, go to the directory where you want DiscordAlertsTrader, e.g.: 
```cd c:\Users\User\Desktop```

Download the package and install it, run the following lines:
```
git clone https://github.com/AdoNunes/DiscordAlertsTrader.git
cd DiscordAlertsTrader
pip install -e .
copy DiscordAlertsTrader/config_example.ini DiscordAlertsTrader/config.ini 
```

Add the **discord token** in config.ini, by default no brokerage is specified. Edit configs, 
for example, chang the authors to follow the trades, change trailing stop, maximum allowed
price difference between alerted and current.  


Run the app by typing:
```DiscordAlertsTrader```
alternatively:
```python -c from DiscordAlertsTrader import gui```


## TDAmeritrade
_______________

*CURRENTLY NO NEW DEVELOPER ACCOUNT UNTIL THE MERGE*

To access the TDAmeritrade account for trading and info is necessary to install 
td-ameritrade-python-api from:

```pip install td-ameritrade-python-api```

Follow the instructions from the github repository to set up an API developer account and get a 
token:
https://github.com/areed1192/td-ameritrade-python-api

once you have your TDA client id, edit config.ini TDA section. There needs to be:

```
[TDA]
client_id = QBGUFGH...
redirect_url = https://127.0.0.1/
credentials_path = secrets_td.json
```

then, run the script:
```python setup_TDA.py```
it will prompt to:

```
$ Please go to URL provided authorize your account: https://auth.tdameritrade.com/auth?response_type=code&redirect_uri=.......OAUTHAP
$ Paste the full URL redirect here:
```

In your browser go to the link, accept TD ameritrade pop-up and copy the link you get re-directed. Once entered you will have your secrets_td.json

## Disclaimer
_________

This is still a Work in Progress project. I get good results using the package, If you plan to use it, **USE AT YOUR OWN RISK**. 

The code and package provided in this repository is provided "as is" and without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the author or contributors be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the code or package or the use or other dealings in the code or package.

Please use this code and package at your own risk. The author and contributors disclaim all liability and responsibility for any errors or issues that may arise from its use. It is your responsibility to test and validate the code and package for your particular use case.

