# Stock Analysis and Optimization with Generative AI

This project leverages Generative AI to perform stock analysis and optimization. It includes various financial metrics and indicators such as RSI, Bollinger Bands, P/E Ratio, Beta, and MACD. Additionally, it uses Modern Portfolio Theory (MPT) and the Black-Litterman Model to optimize portfolios.

## Setup

1. **Install necessary libraries:**
    ```bash
    pip install langchain-openai yfinance PyPortfolioOpt
    ```

2. **API Key:**
    - Obtain an API key from OpenAI.
    - Insert your API key in the notebook where indicated.

## Usage

1. **Initialize the OpenAI LLM:**
    ```python
    llm = initialize_llm(api_key=api_key)
    ```

2. **Define the number of years for analysis:**
    ```python
    years = 2  # Example: 2 years
    ```

3. **List of assets to analyze:**
    ```python
    assets = [
        "Apple (AAPL)",
        "Amazon (AMZN)",
        "Bitcoin (BTC-USD)",
        "Alphabet (GOOGL)",
        "Meta (META)",
        "Microsoft (MSFT)",
        "Nvidia (NVDA)",
        "S&P 500 index (SPY)",
        "Tesla (TSLA)"
    ]
    ```

4. **Fetch and sort tickers:**
    ```python
    query = f"""
    fetch me the tickers from the following assets: {assets}
    Your output must be sorted alphabetically by the ticker and it should be like this:
    tickers = ['AAPL', 'AMZN', 'BTC-USD', 'GOOGL', 'META', 'MSFT', 'NVDA', 'SPY', 'TSLA']
    """
    get_llm_response(llm=llm, prompt=query)
    ```

5. **Calculate start and end dates:**
    ```python
    start_date, end_date = calculate_date_range(years)
    ```

6. **Fetch historical stock data:**
    ```python
    data = yf.download(tickers, start=start_date, end=end_date)
    ```

7. **Plot financial metrics:**
    - RSI
    - Bollinger Bands
    - P/E Ratio
    - Beta
    - MACD

8. **Calculate KPIs:**
    ```python
    kpi_data = calculate_kpis(tickers, start_date, end_date)
    ```

9. **Generate an executive summary with recommendations:**
    ```python
    prompt = f"Read this data {kpi_data} and provide an executive summary with recommendations"
    get_llm_response(llm=llm, prompt=prompt)
    ```

10. **Optimize portfolio using MPT:**
    ```python
    optimal_portfolio = max_sharpe_ratio(mean_returns, cov_matrix, risk_free_rate)
    ```

11. **Optimize portfolio using Black-Litterman Model:**
    ```python
    bl = BlackLittermanModel(S, Q=Q, P=P, pi=market_prior, market_weights=market_prior, risk_free_rate=risk_free_rate)
    ```

## Explanation

- **RSI:** Measures the speed and change of price movements.
- **Bollinger Bands:** Identifies overbought and oversold conditions.
- **P/E Ratio:** Gauges whether a stock is overvalued or undervalued.
- **Beta:** Measures a stock's volatility relative to the market.
- **MACD:** Shows the relationship between two moving averages of a stock’s price.
- **MPT:** Optimizes the portfolio's return for a given level of risk.
- **Black-Litterman Model:** Combines CAPM equilibrium market returns with subjective views for a more stable expected return vector.

## License

This project is licensed under the MIT License.
