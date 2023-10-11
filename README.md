# Trading bot using Alpaca Trading and Lumibot API
This is a quick python tutorial on how to setup a trading bot connected with Alpaca Trading, using Lumibot, allowing to start a trading bot with no actual money, for educational purposes.

**Disclaimer: This tutorial is for educational purposes only and should not be interpreted as trading advice. The provided code and datasets are used for visualization and experimentation purposes and may not represent a realistic trading bot.**

By following the steps below, you'll be able to understand the code and get started with your trading bot project.

## Installation

Step 1: Create an Alpaca Account
First, you'll need to create an account with Alpaca to access their trading API. If you haven't already signed up, you can do so by visiting the Alpaca sign-up page.

Fill out the required information to create your Alpaca account.

Once your account is created, log in to your Alpaca dashboard.

Step 2: Generate API Key and Secret
To connect your trading bot with Alpaca, you'll need to generate an API key and secret. Here's how to do it:

In your Alpaca dashboard, navigate to the "API" section. You can find it in the top navigation bar or in the sidebar menu, depending on the dashboard's layout.
![Generating API Key and Secret](/photo_1.png)

Click on "View API Keys" to generate a new API key and secret pair.
![Generating API Key and Secret](/photo_2.png)

Once generated, make sure to copy and securely store your API key and secret. You won't be able to access the secret again after leaving this page.

Step 3: Configuring Your Trading Bot
With your Alpaca API key and secret in hand, you're now ready to configure your trading bot using the Lumibot framework.
I recommend looking at the "get started" part of the documentation at this stage:
[here](https://lumibot.lumiwealth.com/getting_started.html#getting-started).
# Have a look at lumibot's documentation it explains it all
```bash
#This is before you run the code, assuming you already have python installed (e.g python and command line, or an IDE such as Visual Studio Code with python and its terminal)
pip install lumibot
--------------------------------------------
from lumibot.brokers import Alpaca 
from lumibot.strategies import Strategy
from lumibot.traders import Trader
from lumibot.entities import Asset
ALPACA_CONFIG = {
    "API_KEY": "ENTER_API_KEY",
    "API_SECRET": "ENTER_API_SECRET",
    "ENDPOINT": "https://paper-api.alpaca.markets",
}
class MeanReversionStrategy(Strategy): 
    def initialize(self): 
        self.symbol = "AAPL"
        self.sleeptime = "1M"
    def on_trading_iteration(self):
        if broker.is_market_open():
            last_price = self.get_last_price(self.symbol)
            print(f"Last Price: {last_price:.2f}")
        else:
            print("market is closed")
if __name__ == "__main__":
    broker = Alpaca(ALPACA_CONFIG)
    strategy = MeanReversionStrategy(broker=broker)
    trader = Trader()
    trader.add_strategy(strategy)
    trader.run_all()
```
# Can you figure out what the code from above does?
It retrieves the last price of AAPL from ALPACA trading, it runs every '1M' so every minute...

# What could be next?
Using a higher variety of pre-written functions listed on lumibot's documentation e.g to get out of position, buy, short stocks or even retrive historical data of prices (however this might require you to upgrade to the paid version).
