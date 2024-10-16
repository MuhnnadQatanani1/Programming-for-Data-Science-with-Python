# BikeShare Project - Refactoring

## Overview

This branch contains the refactored code for the **BikeShare** project. The main goal of this refactor was to improve the readability, maintainability, and efficiency of the existing codebase. By breaking down long functions, improving variable and function names, consolidating duplicate code, and applying best practices, we have made the code easier to understand and modify for future improvements.

## Refactoring Goals

- **Improve Readability**: Code is easier to read and understand, especially for new contributors.
- **Enhance Maintainability**: By breaking down large functions and consolidating duplicated code, the code is now easier to maintain and extend in the future.
- **Simplify Logic**: Complex logic was broken into smaller, reusable functions, reducing redundancy.
- **Apply Consistent Naming**: Variables and function names now clearly describe their roles and functionality.
- **Remove Unused Code**: Any code that was not being used has been removed to declutter the project.

## Key Refactoring Changes

### 1. Code Modularization
- **Before**: Long functions were responsible for multiple tasks, making the code difficult to maintain.
- **After**: Functions have been broken down into smaller, reusable pieces. Each function now performs a single, well-defined task.

### 2. Improved Variable and Function Names
- **Before**: Variable and function names were not descriptive enough.
- **After**: All variables and functions have been renamed to clearly indicate their purpose. For example, `available` is now `is_available`, and `calculate_total_cost` has been renamed to `calculate_rental_cost` for clarity.

### 3. Consolidation of Duplicate Logic
- **Before**: Code for checking bike availability was repeated in multiple places.
- **After**: The availability check has been consolidated into a single method, `get_available_bikes`, which is now reused wherever needed.

### 4. Removal of Magic Numbers
- **Before**: Discount rates were hardcoded directly in the functions, making future updates difficult.
- **After**: Constants like `DISCOUNT_RATE_FREQUENT_USER` are used to clearly define important values, making them easier to modify in the future.

### 5. Clean Formatting and Comments
- **Before**: The code was inconsistent in formatting and lacked sufficient comments.
- **After**: The code is now properly formatted with consistent indentation and spacing. Comments have been added to explain complex parts of the code.

## Example of Refactored Code

Here’s a sample of the changes made to the original `calculate_rental_cost` function:

```python
def calculate_rental_cost(self, customer):
    """Calculates the total rental cost for a customer, including discounts."""
    total_cost = 0
    available_bikes = self.get_available_bikes()

    # If no bikes are available, return 0 cost
    if not available_bikes:
        return 0

    for bike in available_bikes:
        total_cost += bike.price_per_hour * customer.hours_rented

    # Apply discount for frequent customers
    if customer.is_frequent_user:
        total_cost = self.apply_frequent_user_discount(total_cost)

    return total_cost
