# Solana Rent Calculator

This simple calculator helps you determine the amount of rent you need to pay for storing data on the Solana blockchain.

## What is Rent in Solana?

In the Solana blockchain, "rent" refers to a small fee that accounts must pay to store data on the network. This mechanism helps prevent the blockchain from becoming bloated with unused accounts and data.

Key points about Solana's rent system:
- Rent is paid in SOL
- Accounts that maintain a minimum balance are exempt from rent
- Rent is collected on certain epochs

## Rent Calculation

The formula for calculating rent is:

```
rent = (number_of_bytes + 128) * bytes_rate
```

Where:
- `number_of_bytes` is the size of the account data
- `128` is a constant overhead for all accounts
- `bytes_rate` is the rent fee per byte-epoch (currently set at 19.055441478439427 lamports per byte-epoch)

## Rent Exemption

An account can be made exempt from rent if it holds at least 2 years worth of rent. This is called the "rent exempt minimum balance". To calculate this:

```
rent_exempt_minimum = rent * 2 * 365
```

## Simple Rent Calculator

Here's a simple Python function to calculate rent and the rent exempt minimum:

```python
def calculate_solana_rent(data_size):
    bytes_rate = 19.055441478439427  # lamports per byte-epoch
    epochs_per_year = 365
    
    rent = (data_size + 128) * bytes_rate
    rent_exempt_minimum = rent * 2 * epochs_per_year
    
    return {
        "rent_per_epoch": rent,
        "rent_exempt_minimum": rent_exempt_minimum
    }

# Example usage
account_size = 1000  # in bytes
result = calculate_solana_rent(account_size)
print(f"Rent per epoch: {result['rent_per_epoch']} lamports")
print(f"Rent exempt minimum: {result['rent_exempt_minimum']} lamports")
```

## Note

Please be aware that the `bytes_rate` may change in the future. Always refer to the official Solana documentation for the most up-to-date information.

## Contributing

Feel free to contribute to this calculator by opening issues or submitting pull requests.

## License

This project is open source and available under the [MIT License](LICENSE).
