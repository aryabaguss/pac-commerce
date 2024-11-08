# PacCommerce Membership System

A Python-based membership system that determines user tiers and calculates discounts based on monthly expenses and income using Euclidean Distance algorithm.

## Features

- Membership tier prediction using Euclidean Distance
- Discount calculation based on membership status
- Display membership benefits and requirements
- User membership status tracking

## Membership Tiers

The system has three membership tiers:

1. **Platinum**
   - 15% discount
   - Includes all Gold & Silver benefits
   - Additional 30% maximum cashback

2. **Gold**
   - 10% discount
   - Includes Silver benefits
   - Online ride-hailing vouchers

3. **Silver**
   - 8% discount
   - Food vouchers

## Membership Requirements

| Tier     | Monthly Expense (Million IDR) | Monthly Income (Million IDR) |
|----------|------------------------------|----------------------------|
| Platinum | 8                            | 15                         |
| Gold     | 6                            | 10                         |
| Silver   | 5                            | 7                          |

## Understanding Euclidean Distance in This System

### What is Euclidean Distance?
Euclidean Distance is a mathematical measure of the straight-line distance between two points in a space. Think of it as measuring the length of a ruler between two points on a graph.

### How We Use It
In this membership system, we use Euclidean Distance to find which membership tier best matches a user's financial profile by:
1. Treating monthly expense and income as coordinates (x,y) on a 2D plane
2. Calculating the distance between the user's position and each tier's requirements
3. Assigning the tier with the shortest distance to the user

### The Math Behind It
Given:
- User's position: (monthly_expense, monthly_income)
- Tier's position: (required_expense, required_income)

```
distance = √[(monthly_expense - required_expense)² + (monthly_income - required_income)²]
```

### Example Calculation
If a user has:
- Monthly Expense: 7 million
- Monthly Income: 12 million

The system calculates distances to:
1. Platinum (8,15): √[(7-8)² + (12-15)²]
2. Gold (6,10): √[(7-6)² + (12-10)²]
3. Silver (5,7): √[(7-5)² + (12-7)²]

The tier with the smallest calculated distance is chosen as the user's membership level.

## How It Works

### Price Calculation

Final price is calculated using the formula:
```
final_price = total_price - (total_price × discount_rate)

Discount rates:
- Platinum: 15%
- Gold: 10%
- Silver: 8%
```

## Usage Example

```python
# Create a membership instance
membership = Membership_user("John")

# Show available benefits
membership.show_benefit()

# Show membership requirements
membership.show_requirements()

# Predict membership tier based on monthly expense and income
membership.predict_membership(7, 12)

# Calculate final price with membership discount
membership.calculate_price("John", [100000, 250000, 300000])
```

## Dependencies

- tabulate
- math

## Error Handling

The system includes basic error handling for:
- Invalid membership status
- Unknown usernames

## Notes

- All monetary values are in millions of Indonesian Rupiah (IDR)
- The system maintains an internal dictionary of user memberships
- Calculations are rounded to 2 decimal places for precision

## Contributing

Feel free to fork this repository and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.