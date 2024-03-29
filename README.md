# Risk-Parity-Portfolio

The goal of the project is to construct a simple risk parity portfolio. On a purist perspective, a risk parity portfolio means that there is an equal contribution of risk from each security in one's portfolio. For example, if one has 8 securities of in his portfolio, the contribution from each security must be the same. Note that I am referring to individual security level but not the portfolio level at a broader sense. The portfolio volatility as a whole might be greater, equal or smaller than the volatility of each security depending the correlation of return across each security.

In terms of security selection, I have selected 7 securities. 3 of them are REITs, 1 of them is a family office that has a heavy exposure to private equity and the remaining ones are growth stocks from various industries. There is no specific preference in terms of market cap, liquidity, style of the stocks selected as the whole purpose of this exercise is to demonstrate the prospect of the risk parity strategy. Therefore, the 3 growth stocks are chosen because of their higher volatilities. This is essential to implement risk parity strategy effectively as it amplifies one's allocation to an asset that has a lower volatility and reduces one's allocation to risky assets at the same time.

## Source of Data

All daily stock performance data is extracted directly and annualised from Yahoo Finance using the "Datareader" method from the Pandas package.

## Portfolio Construction Methodology

![](Portfolio%20Construction%20Methodology.PNG)

To understand the risk parity strategy, we need to first determine the target volatility at portfolio level. The level of target volatility is subjective in nature. Depending on each investor's risk appetite, he may choose a number that is in-between the volatility of all different types of asset classes in a portfolio.

Assume that there is an investor who wants to include 5 stocks and 5 bond securities in their portfolio. Assume that the average volatility per stock was estimated to be 0.15 p.a. and the volatility per bond was estimated to be 0.05 p.a.. If he wants a portfolio which has a higher return than holding bonds solely but less risky thatn holding stocks entirely, he may pick a number in the middle, which is 0.10. If the investors wants more risk, he will pick a number that is slightly higher than 0.10, say 0.12 or 0.13. For simplicity, I have assumed my target volatility as 0.10 p.a..

Since there are seven securities in the portfolio, the risk budget is obtained by simply dividing our target volatility by the number of securities of the portfolio. Risk budget and Risk Contribution are interchangable terms. The risk contribution is the product of annualized volatility over 250 trading days (col.2) and the portfolio weights adjusted according to the volatility per security (col.3).

The 'Port_w' column is the weight allocation adjusted by the repsective volatilities, the lower the value in column 'A_Eq_Vol',the higher the value in 'Port_w" column. However, the sum of this column does not add up to 1. Thais is why the 'F_Port_w' exists. We multiply the 'Port_w' column with a normalizing factor to generate the values in the 'F_Port_w' column (col.4).

The right most column is just a product between the 'F_Port_w' column and the 'A_Eq_R', for which the latter is the annualized daily returns of each stock. The column calculates the expected return in each security depending on the allocation of our money.


## Summary of Findings

![](Performance%20Results%20Table.PNG)

The performance is encouraging. The annualized returns of our stock selection has outperformed the benchmarks by a wide margin. Risk Parity approach has the second lowest return compared to allocation strategies with the same 7 securities. The same goes for the volatility of the portfolio.

However, the annualized standard devidation is only 1% higher than the Min. Variance Portfolio, but in return we gain 4% more excess return in the same year. Excess Return is defined as the Annualized Return minus the latest 10 years US Treasury Yield. This has practical implications, as the Min. Variance Portfolio is often criticised by academics as unpractical where extreme weights is often observed in the optimization process.

In contrast with the Equal Weighting Strategy, Risk Parity Strategy is slightly less risky, but it has underperformed by ~6%. The reason for that is the latter has underweighted Docusign significantly, while the Equal Weight Strategy has twice the exposure. The off the charts return of 85% is going to have huge impact on return in situations like that. Finally, the Max. Sharpe Portfolio, also known as the most efficient portfolio, has generated the greatest return with the greatest exposure as well.

## Limitations and Further Research
First of all, the comparison with benchmark indices is not entirely fair as the exposures to regions and industries are very different from my portfolio. Stock styles such as momentum, size, value and liquidity are also ignored. Further studies can be conducted to construct a much a larger portfolio that matches more closely to the benchmark chosen.

Secondly, I use daily share prices as the basis of the analysis. However, it may contain too much noises and hence affect the representativeness of the stock return and volatility. The same analysis can be conducted by using weekly/ monthly data instead. However, this requires more sophisticated techniques such as front-filling blanks.

Thirdly, along the same line of reasoning, the modeling of the volatility is particularly important to the implementation of the Risk Parity Strategy. More recent events, especially the ones that has material impact on the economy such as COVID-19 should be given a higher weight. It will be interesting to re-run the analysis using EMWA, GARCH techniques in modeling the portfolio volatilies.
