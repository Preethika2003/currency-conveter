# currency-conveter
#currency converter
import requests

# Function to get exchange rates
def get_exchange_rate(base_currency, target_currency):
    url = f"https://api.exchangerate-api.com/v4/latest/{base_currency}"
    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        if target_currency in data["rates"]:
            return data["rates"][target_currency]
        else:
            print("Invalid target currency!")
            return None
    else:
        print("Error fetching exchange rates.")
        return None

# Function to convert currency
def convert_currency(amount, base_currency, target_currency):
    rate = get_exchange_rate(base_currency, target_currency)
    if rate:
        converted_amount = amount * rate
        return converted_amount
    return None

# User input
amount = float(input("Enter amount: "))
base_currency = input("Enter base currency (e.g., USD, INR, EUR): ").upper()
target_currency = input("Enter target currency (e.g., USD, INR, EUR): ").upper()

converted_amount = convert_currency(amount, base_currency, target_currency)

if converted_amount:
    print(f"{amount} {base_currency} = {converted_amount:.2f} {target_currency}")

