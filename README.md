# Financial Planning using Monte Carlo

## Background

You decided to start a FinTech consultancy firm, and you want to make a difference by working on projects with high social impact in local communities. They want to create a tool that helps their members enhance their financial health. The Chief Technology Officer (CTO) of the credit union asked you to develop a prototype application to demo in the next credit union assembly.

The credit union board wants to allow the union's members to assess their monthly personal finances, and also be able to forecast a reasonably good retirement plan based on cryptocurrencies, stocks, and bonds.

In this project I focused on using APIs as part of the technical solution - to create two financial analysis tools.

The first will be a personal finance planner that will allow users to visualize their savings composed by investments in shares and cryptocurrencies to assess if they have enough money as an emergency fund.

The second tool will be a retirement planning tool that will use the Alpaca API to fetch historical closing prices for a retirement portfolio composed of stocks and bonds, then run Monte Carlo simulations to project the portfolio performance at 30 years. You will then use the Monte Carlo data to calculate the expected portfolio returns given a specific initial investment amount.

### Resources

This project will utilize two APIs:

* The **Alpaca Markets API** will be used to pull historical stocks and bonds information.  
    
* The **Alternative Free Crypto API** will be used to retrieve Bitcoin and Ethereum prices.

## Instructions

### Part 1 - Personal Finance Planner

In this portion of the project I created a personal finance planner application, under the following assumptions:

* The average household income for each member of the credit union is $12,000.

* Every union member has a savings portfolio composed of cryptocurrencies, stocks and bonds:

    * Assume the following amount of crypto assets: `1.2` BTC and `5.3` ETH.

    * Assume the following amount of shares in stocks and bonds: `50` SPY (stocks) and `200` AGG (bonds).

#### Collect Crypto Prices Using the `requests` Library

1. Create two variables called `my_btc` and `my_eth`. Set them equal to `1.2` and `5.3`, respectively.

2. Use the `requests` library to fetch the current price in US dollars of bitcoin (`BTC`) and ethereum (`ETH`) using the **Alternative Free Crypto API** endpoints provided in the starter notebook.

3. Parse the API JSON response to select only the crypto prices and store each price in a variable.

4. Compute the portfolio value of cryptocurrencies and print the results
> The current value of your 1.2 BTC is $31254.00
> The current value of your 5.0 ETH is $1820.98

#### Collect Investments Data Using Alpaca: `SPY` (stocks) and `AGG` (bonds)

1. Create two variables named `my_agg` and `my_spy` and set them equal to `200` and `50`, respectively.

2. Set the Alpaca API key and secret key variables, then create the Alpaca API object using the `tradeapi.REST` function from the Alpaca SDK.

3. Format the current date as ISO format. You may change the date set in the starter code to the current date.

4. Get the current closing prices for `SPY` and `AGG` using Alpaca's `get_barset()` function

5. Pick the `SPY` and `AGG` close prices from the Alpaca's `get_barset()` DataFrame response and store them as Python variables

6. Compute the value in dollars of the current amount of shares and print the results
> The current AGG closing price is: $107.1
> The current SPY closing price is $452.11

#### Savings Health Analysis

In this section, I assessed the financial health of the credit union's members.

1. Create a variable called `monthly_income` and set its value to `12000`.

2. To analyze savings health, create a DataFrame called `df_savings` with two rows. Store the total value in dollars of the crypto assets in the first row and the total value of the shares in the second row.

3. Use the `df_savings` DataFrame to plot a pie chart to visualize the composition of personal savings.

![image](https://user-images.githubusercontent.com/98990090/172505681-83f87c33-6462-42a7-889f-3f6a9a07a46b.png)

4. Use `if` conditional statements to validate if the current savings are enough for an emergency fund. An ideal emergency fund should be equal to three times your monthly income.

![image](https://user-images.githubusercontent.com/98990090/172505722-e8c82b97-0956-4f72-8944-91c641e6df88.png)

### Part 2 - Retirement Planning

In this section, I used the Alpaca API to fetch historical closing prices for a retirement portfolio and then used the MCForecastTools toolkit to create Monte Carlo simulations to project the portfolio performance at `30` years.

#### Monte Carlo Simulation

1. Use the Alpaca API to fetch five years historical closing prices for a traditional `40/60` portfolio using the `SPY` and `AGG` tickers to represent the `60%` stocks (`SPY`) and `40%` bonds (`AGG`) composition of the portfolio.
2. 
3. Configure and execute a Monte Carlo Simulation of `500` runs and `30` years for the `40/60` portfolio.

3. Plot the simulation results and the probability distribution/confidence intervals.

![image](https://user-images.githubusercontent.com/98990090/172505783-a71d0ecf-b6bd-4ee7-a7cc-ccce759c0d43.png)
![image](https://user-images.githubusercontent.com/98990090/172505760-199cffab-5f2b-4aa8-824d-242e7d0f4e68.png)


#### Retirement Analysis

1. Fetch the summary statistics from the Monte Carlo simulation results

2. Given an initial investment of `$20,000`, calculate the expected portfolio return in dollars at the `95%` lower and upper confidence intervals.
> There is a 95% chance that an initial investment of $20000 in the portfolio over the next 30 years will end within in the range of $62784.26 and $792020.15

3. Calculate the expected portfolio return at the `95%` lower and upper confidence intervals based on a `50%` increase in the initial investment.
> There is a 95% chance that an initial investment of $45000.0 in the portfolio over the next 30 years will end within in the range of $141264.59 and $1782045.33
