# EXECUTE Phase Instructions

## Your Task
You have 15-25 minutes to implement a working Discount Engine Validator based on your plan.

## Implementation Requirements

### Language Constraints
- **Preferred**: Node.js (JavaScript)
- **Alternative**: Python
- **No external libraries/APIs** - use only standard library functions
- Single file solution preferred for simplicity

### Input Files
This folder contains the exact test data your solution must process:
- `orders.csv` - Order data with columns: order_id, customer_id, amount, date, coupon_code
- `coupons.json` - Coupon definitions with discount rules and expiration dates

### Expected Output
Your solution must generate:

1. **results.csv** with columns:
   - order_id
   - original_amount
   - final_amount  
   - coupon_code
   - discount_amount
   - status (applied, rejected, expired, invalid, none)
   - message (explanation for the status)

2. **summary.md** - A markdown report containing:
   - Total orders processed
   - Breakdown by status
   - Total revenue impact
   - Example entries for each status type

### Key Technical Requirements
Based on the requirements you extracted, ensure your implementation:
- Handles case-insensitive coupon matching
- Strips/trims whitespace appropriately
- Manages the $0.50 payment minimum correctly
- Implements proper expiration date checking
- Calculates discounts accurately (percentage vs amount off)
- Handles edge cases gracefully

### Where to Code
**Create your implementation in the `/src` directory** (at the repository root, not in docs).

### Testing Your Solution
Run your solution against the provided test files:
```bash
# For Node.js
node src/your_solution.js

# For Python
python src/your_solution.py
```

### Evaluation Criteria
Your implementation will be assessed on:
- **Correctness**: Does it produce accurate results?
- **Completeness**: Does it handle all requirements and edge cases?
- **Code Quality**: Is it clean, readable, and well-structured?
- **Robustness**: Does it handle errors gracefully?
- **Output Format**: Are the CSV and markdown outputs properly formatted?

### Tips
- Start with the core functionality, then add edge cases
- Test incrementally as you build
- Use clear variable names and logical flow
- Remember to handle all status types correctly
- Don't forget proper CSV parsing/writing
- Pay attention to number formatting (2 decimal places for currency)

### Common Pitfalls to Avoid
- Number precision in financial calculations
- Edge cases in data validation
- Date/time handling considerations
- Business rule enforcement
- Output format compliance

## Time Management
You have 15-25 minutes. Suggested breakdown:
- 5 minutes: Setup and file I/O
- 10 minutes: Core validation logic
- 5 minutes: Edge cases and output formatting
- 5 minutes: Testing and refinement

Good luck!