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

## Test Cases

The program includes several test cases to demonstrate the different functionalities of the Paccommerce Membership System.

### Test Case 1: Displaying Membership Benefits

```python
user1 = Membership_user('Cahya')
user1.show_benefit()
```

This test case shows how a user can view the details of the available Paccommerce membership benefits, including the discount rates and additional perks for each tier.

### Test Case 2: Displaying Membership Requirements

```python
user1.show_requirements()
```

This test case demonstrates how a user can view the monthly expense and income requirements for each Paccommerce membership tier.

### Test Case 3: Predicting Membership Tier

```python
user2 = Membership_user('Shandy')
user2.predict_membership(3, 10)
```

This test case shows how the system uses Euclidean Distance to predict a user's membership tier based on their monthly expense and income. The output displays the calculated distances for each tier and the predicted membership.

### Test Case 4: Calculating Discounted Price

```python
user1.calculate_price(user1.username, [150000, 200000, 400000])
```

This test case verifies the functionality of the `calculate_price()` method, which calculates the discounted final price for a user's purchase based on their membership tier.

### Test Case 5: Handling Unknown Users

```python
user_bambang = Membership_user("Bambang")
user_bambang.predict_membership(3, 4)
user_bambang.show_membership(user_bambang.username)
user_bambang.calculate_price(user_bambang.username, [300_000, 150_000, 1_250_000, 15_000])
```

This test case demonstrates how the system handles cases where the user is not found in the internal user data dictionary. It shows the system's behavior when predicting a membership tier, displaying the membership, and calculating the price for an unknown user.

## Contributing

Feel free to fork this repository and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.