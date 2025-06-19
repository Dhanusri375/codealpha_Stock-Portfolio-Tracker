# Stock Portfolio Tracker

# Hardcoded stock prices
stock_prices = {
    "AAPL": 180,
    "TSLA": 250,
    "GOOGL": 130,
    "AMZN": 120
}

# Function to calculate total investment
def calculate_total_investment():
    total_investment = 0
    portfolio = {}

    print("Enter your stocks (type 'done' to finish):")
    while True:
        stock = input("Enter stock symbol (e.g., AAPL): ").upper()
        if stock == 'DONE':
            break
        if stock not in stock_prices:
            print("Stock not found in price list.")
            continue
        try:
            quantity = int(input(f"Enter quantity for {stock}: "))
        except ValueError:
            print("Invalid quantity. Please enter a number.")
            continue

        portfolio[stock] = portfolio.get(stock, 0) + quantity
        total_investment += stock_prices[stock] * quantity

    return portfolio, total_investment

# Function to save result
def save_to_file(portfolio, total, filename="result.txt"):
    with open(filename, "w") as file:
        file.write("Your Stock Portfolio:\n")
        for stock, qty in portfolio.items():
            file.write(f"{stock}: {qty} shares @ {stock_prices[stock]} = ₹{qty * stock_prices[stock]}\n")
        file.write(f"\nTotal Investment Value: ₹{total}\n")
    print(f"\nResult saved to {filename}")

# Main
if __name__ == "__main__":
    user_portfolio, total = calculate_total_investment()
    print("\n📈 Your Portfolio Summary:")
    for stock, qty in user_portfolio.items():
        print(f"{stock}: {qty} shares x ₹{stock_prices[stock]} = ₹{qty * stock_prices[stock]}")
    print(f"\n💰 Total Investment: ₹{total}")

    choice = input("\nDo you want to save the result to a file? (yes/no): ").lower()
    if choice == "yes":
        save_to_file(user_portfolio, total)
