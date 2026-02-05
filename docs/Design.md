# Lovable Trades
A Market and Stock Analysis and Backtesting Application

The app uses mathematical tests based on different market data, technical analysis and price movements to score the market and individual stocks.
The main goal of the app is to develope a system that has the capability of predictive price movement direction that is better than random selection. 
The program is designed to optimize itself or with help from the user to improve the performance by time and deliver more win rate with higher scores.
In combination with alerts and other ai assessment help, it helps the user find good trading opportunities by direct signals or indirect delivery of useful information.
Another important role of the app is backtesting the scoring systems. It runs the analysis on existing data from the past, and uses that to improve the accuracy of the tests.
The app provides these results through a few pages. 

The app development is done in three phases. But the foundation, database setup, design elements and capabilities should be prepared and built considering all the phases of
development regardless of what module is activated or created at what point. Each phase is activated and tested before the second phase is. Creating, updating and activating the new
phases must not require recreating the app, or change of its structure. The three phases of the app are:

* Analysis (running the scoring tests for stocks and market on a daily basis
* Backtetsting. Running the scoring system in days in the past and reporting the perforrmance of the stocks and market overall and the relationship of that peformance and the scores.
* Optimization. The process of updating and modifying the system, to improve the corelatin between scores and price movements.

While pages are described below, create the pages for the app, but DO NOT design them until the instructions specifically explain the design and what is needed. This will be an ongoing process.

## Pages

* Analysis
The main page of the app that is the starting point. User enters or uploads the list of symbols and the app runs the tests to score and deliver the results in this page.
The main tests that are run on this page are SA (Stock Analysis) and MC (Market Condition) scoring systems. 

* Backtesting
This page runs the same analysis and scoring as the Stock Analysis page but on days in the past and shows the results and compares it with how stocks did and how corelated scores and price movements are.

Matrices
A set of tables that populates results of multiple stocks in a single day, or a single stock or market conditioin in several days. 
The data is delivered via an organized table, as well as visual charts and can be exported into a CSV file. Data includes total scores, score breakdowns, 
and stock price performance during preset times from the analysis date into the future of that day. The matrices help the optimmization process. 
There are three sub-pages currently one for each matrix:

- Score Matrix
Score matrix compares the performance of a group of stocks in a specific date in the past. The page deliveres the scores, the breakdown of each question and point,
as well as gain/loss report within different time periods after the analysis date. For example, if the analysis is run for Oct 1st, 2025. Gain/Loss is measured for Nov 1st, 2025.
Usign the matrix could tell the user buying stocks with over 75% score results in 90% win rate within one month of the investment if MC is over 50%.

- Stock Matrix
This matrix compares the performance of a stock for a set amount of time during a period of time. So, the report is for one stock, its daily score, and its monthly (or any other) gain and
loss a month after that date. Then the score, and performance is compared to determine the corelation between score and gain, and, the timing of investment in relation to score changes.
The test can tell the user that the best time to buy a stock is when there are three days of 'blue' score bars in a row (or three days of SA score over 65).

- Market Matrix
This matrix uses the QQQ ETF as the proxy for market evaluation. The table shows the MC Score for each day during the analysis period, and how that score did in a set period of time.
Then it compares the relatinship between scores and gains, as well as the timing of potential investment and its relationship to score changes. For example, the result could show the
best time to buy QQQ is when the MC score is above 70% and right after the score has moved 5% up. And best time to sell it, is the day after it drops below 55%.


Optimization
These pages are designed to enable the system to optimize itslef. The optimization is done via multiple methods from manual, to assisted to fully automated. 
In development of the app, we will work and develope these pages in phases. The initial phase is focused on manual optimization that is performaed by using the CSV files
from matrices and determining the corelation between scores of each test, individual questions and points given with the price movements of the stock within set time periods.

- Manual Optimization
This is when the system uses 'saved matrices analysis results' to compare the corelation between price movements and scores given. The goal is that higher scores result in higher average
gain and higher win rate. In other words, a groups of stocks with score of over 80 should do better in a month that stocks with scores of 50-60. In this level, the ai looks at individual
questions and points and determines what questions are best corelated and which ones are not, and the usere decides how to change the config of the scoring to improve the results. Further
analysis then confirms or suggest more modification. The exact design of this page is TBD.
  
- Semi-Automated Optimization
This page is dedicated to an optimization process that is semi-automated. In other words, the first step of analysis is run like the manual optimization, but, instead of the user deciding
how to change the scoring system, weight, or adding or removing question, the app makes that decision, runs the tests and reports the results to the user. The app may continue improving the
tests indefinetly as new data from different stock groups and different time periods are added to the analysis batch.

- Automated Optimization
In full automation, the system starts from creating watchlists randomly or based on user defenitions. Run analysis on them randomly first and based on important events and price movements history to
make sure all edgecases are covered. In each round, the system updates the scoring systems. This is done for both SA test and then MC test independently. Then, the analysis is run for the combination
of the two and the formulas that are used for Master Score and other decision making points like alerts effects, or tiers and fund allocation. This is a theoritical phase at this point and the
first step includes defining the parameters of the test.


Lists
This page contains different saved 'lists' for future access. Including watchlists, analysis results, matrix results and other potential lists in the future.

Setting
This page includes optional settings that include but not limited to colors, limits and thresholds, api keys, and design elements.

Config
Config pages include the scoring systems, questions, points and calculations. Config allows updating and addition of scores, questions, point systems and formulas.

---

PAGE DESIGNS

# Main header (Repeated on all pages)
- LOVABLE TRADES logo or title on the left
- Navigation menu on the right. Including links 
| Analysis | Backtest | Lists | Matrix (submenu >> Market > Stock > Score) | Optimization (sub menu >> Manual > Semi-Auto > Automated ) | Cog Icon (sub menu >> Setting > Config )

# Main Footer
Main links in a row. 
Below that: LOVABLE TRADES (R) - BY SEAN FAHIMI - COPYRIGHT 2026


Page contents

ANALYSIS PAGE

### TOP ROW (Analysis form)
This row includes the main form to enter or upload the list of stocks that the user wants to run the analysis for. The QQQ or MC score is automatically run when the analysis is run.
The row includes the text bar to enter the symbols. An upload icon that can be used to upload the list of symbols. Watchlist dropdown that allows selecting a list, adding and/or editing
one as well as saving the one that was just analyzed. Then the Analyze button that starts the analysis. And then the 'Backtesting' button that activates, or moves the user to the backtesting mode/page. 

### Analysis Table

Rows:
1. Table headings
2. MC (Market Condition) - All data is from QQQ as MC proxy. Details Below
3. Stocks details rows showing the SA test result for all the stocks in the searched list (details below)
4. Beta row with the purpose of comparing the performance of the list with the market (QQQ) (details below)

Table Details:
Col 1
Checkbox (circle shape)
Selecting the checkbox displays buttons on top of the table for:
 - Add to watchlist
 - Remove from watchlist
 - Stock Matrix
 - Score matrix if multiple checkboxes are selected

MC: Check box that opens button for 'MC Matrix'
BETA: ---

Col 2
Symbol 
Design: Size: 18px in white allcap text
Second Line: Company sector and Name in small gray font. Truncated after two words
Toggle to Company Summary. 

MC: QQQ
BETA: BETA

Col 3
SA Score 
Design: In a circle with SA color coded background based on the score.
Toggle to: Breakdown of the answers and points given

MC: MC Score
BETA: 

Col 4
Alert Icon
Design: Alert Icon in red/green/yellow based on the type of alert. If multiple alerts, pick the higher urgency color
Toggle: List of alerts and description of them

MC: Market Alerts
BETA: ---

Col 5:
Tier + Max Portfolio % Limit separated with a '.'
Design: Reactangle with background of tiers colors. All buttons save width regardless of content width
Tooltip: Show the Tier defenitin about the company

MC: T1 . $200k
BETA: ---

Col 6:
MS Score
Design: Transparent equare with rounded borders, with 0.5 px and number in MS color coding
Toggle: How the MS Contrarian Score is calulated. Also show VIX

MC: ---
BETA: ---

Col 7:
MS Signal
Design: Rectangle transparent with border and text in signal color code. All recangles to have the same width regardless of text width

MC: MC Level Signal
BETA: ---

Col 8:
Price (todays)
2nd Line: After-Hour % change in small text if any
Toggle: Details of price change % for 1d, 5d, 1m, 3m, 1yr a vertical separator then after-hour - change 1 day ago, change 2 days ago, change 3 days ago, change 4 days ago

MC: QQQ Price
Toggle: Details of price change % for 1d, 5d, 1m, 3m, 1yr a vertical separator then after-hour - change 1 day ago, change 2 days ago, change 3 days ago, change 4 days ago
BETA: ---

Col 9: 
1-Day price change % (live during market hours or after hours if available)

MC: QQQ 1-Day price change %
BETA: Average % of stocks in the table

Col 10:
5-Day price change %

MC: QQQ 5-Day price change %
BETA: Average % of stocks in the table

Col 11:
1M price change %

MC: QQQ 1M price change %
BETA: Average % of stocks in the table

Col 12:
3M price change %

MC: MC Score
BETA: Average % of stocks in the table


---

PAGE DESIGN
Backtesting

The backtesting page is mostly identical to the Analysis page. Below are the differences:

The main row (the analysis form) is the same, with one difference. Instead of the Backtesting button, there is a calendar form with arrows.
There is also an X icon that takes the user back to the main analysis page

The table is identical except the Price Change columns. There are only three columns for price change %. 5D, 1M and 3M
The important difference is that these are not days in the past. These are days in the FUTURE in relation to the analysis date.
The date selected to run the backtest is in the past. Therefore we want to know how the stock did after. So, we need to calculate 
the dates from the analysis date to learn how the stock did in a month for example. The formula is Date of Analysis, Plus (time period)

---

Other pages.

Create the title of the other pages. But do not design them. 
Pages that are waiting to be designed are 
Matrix pages. Optimization Pages. 

Only design pages that you have description for

For Setting and Config pages, create your design that matches the rest of the app. 


























