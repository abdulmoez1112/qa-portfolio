# Test Cases: Product Sorting and Cart Edge Cases (saucedemo.com)

Scripted test cases for the product list and cart of the practice app https://www.saucedemo.com. Account for all cases unless stated: standard_user / secret_sauce. Status is "Not run" until a run is logged in the results table of a test cycle.

## Sorting

| ID | Title | Preconditions | Steps | Expected result | Priority |
|---|---|---|---|---|---|
| TC-SORT-01 | Default sort is Name (A to Z) | Logged in, on /inventory.html | 1. Read the sort dropdown. 2. Read product names top to bottom. | Dropdown shows "Name (A to Z)". Names are in ascending alphabetical order. | High |
| TC-SORT-02 | Sort by Name (Z to A) | On product list | 1. Choose "Name (Z to A)" from the dropdown. 2. Read product names top to bottom. | Names are in descending alphabetical order. The first product is "Test.allTheThings() T-Shirt (Red)". | High |
| TC-SORT-03 | Sort by Price (low to high) | On product list | 1. Choose "Price (low to high)". 2. Read prices top to bottom. | Prices ascend. The first product is the cheapest ($7.99) and the last is the most expensive ($49.99). | High |
| TC-SORT-04 | Sort by Price (high to low) | On product list | 1. Choose "Price (high to low)". 2. Read prices top to bottom. | Prices descend. The first product is $49.99 and the last is $7.99. | High |
| TC-SORT-05 | Sort order survives adding to cart | Sorted by Price (high to low) | 1. Click "Add to cart" on the first product. 2. Check list order and button label. | List order does not change. The clicked product shows "Remove". Cart badge shows 1. | Medium |
| TC-SORT-06 | Sort selection after returning from a product page | Sorted by Price (low to high) | 1. Open any product by clicking its name. 2. Click "Back to products". 3. Check the dropdown and list order. | Record the actual behavior. Expected: list is shown in a consistent order and the dropdown label matches the order displayed. | Medium |

## Cart edge cases

| ID | Title | Preconditions | Steps | Expected result | Priority |
|---|---|---|---|---|---|
| TC-CART-01 | Cart badge count matches items added | Empty cart | 1. Add three different products. 2. Read the badge. 3. Open the cart. | Badge shows 3. Cart lists the same three products with quantity 1 each. | High |
| TC-CART-02 | Remove an item from the cart page | Two products in the cart | 1. Open the cart. 2. Click "Remove" on one product. | The product disappears from the list. Badge shows 1. The other product stays. | High |
| TC-CART-03 | Cart persists after navigating away and back | Two products in the cart | 1. Click "Continue Shopping". 2. Open the cart again. | Both products are still in the cart. Badge still shows 2. | Medium |
| TC-CART-04 | Checkout with an empty cart | Empty cart, logged in | 1. Open the cart. 2. Click "Checkout". 3. Fill first name, last name, postal code. 4. Continue. | Record the actual behavior. Expected by most shops: checkout is blocked or warned for an empty cart. Log a bug if the order can be completed with zero items. | High |

## Notes

- Sorting cases use the four options in the dropdown: Name (A to Z), Name (Z to A), Price (low to high), Price (high to low).
- For problem_user, error_user and visual_user, repeat the sorting cases and compare with standard_user. See BR-001 to BR-006 for issues already found with those accounts.
- TC-SORT-06 and TC-CART-04 are written as "record the actual behavior" cases because the pass criteria depend on what the app does; update Expected and add a bug report after the first run.
