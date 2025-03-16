# tradingbot-python
This is a python trading robot which can take trading strategies and execute them in an automated fashion with minimal or limited interaction

<br>
The strategy is simple, it uses the Binance.client library to access real-time data of the asset to analyze, you can install all the requirements in the requirements.txt

The calculate_rsi() function calculates the value of RSI to use it in the strategy. Backtest_strategy() uses the following parameters: Inital bank, which is the money the user will use for testing the strategy. Percentages for TPs, where the user will adjust them depending on the asset they want to test the strategy on. Percentages for SL, very important to keep the drawdown low and maintain a management risk and security on the position/bank balance. Depending on the asset and risk management of the user, the SL will be higher or lower. RSI values for buys, the user will set these values depending on where the bot will start executing the trades, which also depends on the asset and timeframe used. RSI values for TPs, is if the percentage for TPs doesn't reach their targets but does trigger the value of RSI TPs, a sell trade will be executed to avoid loss on profits or on the position. I will explain later on why this is necessary.

With that been said, lets move on the explanation of how the strategy works: The user will choose an asset to analyze, change the parameters adjusted to his risk management. I'll give you an example to be clearer. Lets look at AVAX/USDT for example, in the 1min timeframe and with these parameters:

Initial Bank: 1000

RSI values for the buys:

First buy at RSI value: 29

Second buy at RSI value: 27.5

Third buy at RSI value: 26

Values in TPs:

First TP percentage: 0.75%

Second TP percentage: 1.75%

First RSI TP value: 55

Second RSI TP value: 65

Values in SL:

SL percentage: -2%

The bot executes 3 buy trades, the first one with 40% of the bank whenever the RSI on the 1min timeframe goes below 29, always after closure of the previous candle. The second on if the RSI goes below 27.5 with 50% of the remaining bank balance and the last buy would be if RSI value goes below 26. If the RSI value of the previous candle is 29.6 for example and the next one is 25.7, the bot goes full position in that candle because it has triggered all buy parameters. This is the code section for the buy signals:

