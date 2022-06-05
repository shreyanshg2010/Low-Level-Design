## Introduction

An Online Stock Brokerage System facilitates its users the trade (i.e. buying and selling) of stocks online. 
It allows clients to keep track of and execute their transactions, and shows performance charts of the different stocks in their portfolios. 
It also provides security for their transactions and alerts them to pre-defined levels of changes in stocks, without the use of any middlemen.
The online stock brokerage system automates traditional stock trading using computers and the internet, making the transaction faster and cheaper. 
This system also gives speedier access to stock reports, current market trends, and real-time stock prices.


## System Requirements

We will focus on the following set of requirements while designing the online stock brokerage system:
1. Any user of our system should be able to buy and sell stocks.
2. Any user can have multiple watchlists containing multiple stock quotes.
3. Users should be able to place stock trade orders of the following types: 1) market, 2) limit, 3) stop loss and, 4) stop limit.
4. Users can have multiple ‘lots’ of a stock. This means that if a user has bought a stock multiple times, the system should be able to differentiate between different lots of the same stock.
5. The system should be able to generate reports for quarterly updates and yearly tax statements.
6. Users should be able to deposit and withdraw money either via check, wire or electronic bank transfer.
7. The system should be able to send notifications whenever trade orders are executed.


## Use Case Diagram

We have three main Actors in our system:
1. **Admin:** Mainly responsible for administrative functions like blocking or unblocking members.
2. **Member:** All members can search the stock inventory, as well as buy and sell stocks. Members can have multiple watchlists containing multiple stock quotes.
3. **System:** Mainly responsible for sending notifications for stock orders and periodically fetching stock quotes from the stock exchange.

Here are the top use cases of the Stock Brokerage System:
1. **Register new account/Cancel membership:** To add a new member or cancel the membership of an existing member.
2. **Add/Remove/Edit watchlist:** To add, remove or modify a watchlist.
3. **Search stock inventory:** To search for stocks by their symbols.
4. **Place order:** To place a buy or sell order on the stock exchange.
5. **Cancel order:** Cancel an already placed order.
6. **Deposit/Withdraw money:** Members can deposit or withdraw money via check, wire or electronic bank transfer.



## Class Diagram

Here are the main classes of our Online Stock Brokerage System:
1. **Account:** Consists of the member’s name, address, e-mail, phone, total funds, funds that are available for trading, etc. We’ll have two types of accounts in the system: one will be a general member, and the other will be an Admin. The Account class will also contain all the stocks the member is holding.
2. **StockExchange:** The stockbroker system will fetch all stocks and their current prices from the stock exchange. StockExchange will be a singleton class encapsulating all interactions with the stock exchange. This class will also be used to place stock trading orders on the stock exchange.
3. **Stock:** The basic building block of the system. Every stock will have a symbol, current trading price, etc.
4. **StockInventory:** This class will fetch and maintain the latest stock prices from the StockExchange. All system components will read the most recent stock prices from this class.
5. **Watchlist:** A watchlist will contain a list of stocks that the member wants to follow.
6. **Order:** Members can place stock trading orders whenever they would like to sell or buy stock positions. The system would support multiple types of orders:
   - **Market Order:** Market order will enable users to buy or sell stocks immediately at the current market price.
   - **Limit Order:** Limit orders will allow a user to set a price at which they want to buy or sell a stock.
   - **Stop Loss Order:** An order to buy or sell once the stock reaches a certain price.
   - **Stop Limit Order:** The stop-limit order will be executed at a specified price, or better, after a given stop price has been reached. Once the stop price is reached, the stop-limit order becomes a limit order to buy or sell at the limit price or better.
11. **OrderPart:** An order could be fulfilled in multiple parts. For example, a market order to buy 100 stocks could have one part containing 70 stocks at $10 and another part with 30 stocks at $10.05.
12. **StockLot:** Any member can buy multiple lots of the same stock at different times. This class will represent these individual lots. For example, the user could have purchased 100 shares of AAPL yesterday and 50 more stocks of AAPL today. While selling, users will be able to select which lot they want to sell first.
13. **StockPosition:** This class will contain all the stocks that the user holds.
14. **Statement:** All members will have reports for quarterly updates and yearly tax statements.
15. **DepositMoney & WithdrawMoney:** Members will be able to move money through check, wire or electronic bank transfers.
16. **Notification:** Will take care of sending notifications to members.






