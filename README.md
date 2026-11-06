# About Purchase Calculator
This application provides a fast and convenient way to total purchases and calculate 
change, reducing manual calculation errors and speeding up the checkout process.

# Features
Simple and user-friendly interface for fast checkout calculations.
- Add multiple purchased items with their prices.
- Automatically calculate the total purchase amount.
- Enter the amount paid by the customer.
- Allow purchase amount adjustment. 
- Instantly calculate the change due.

# How It Works
1. Enter each purchased item and its price.
1. The application automatically updates the running total.
1. After all items have been entered, input the payment amount.
1. Make adjustment to purchase amount.
1. The application calculates and displays the change to be returned to the customer.

# Use Cases
- Quick cashier assistance without a full POS system
- Small vegetable and fruit stands
- Farmers' markets
- Local shops
- Personal expense calculations

# Example
| Item         | Price | Step |
| :----------- | ----: | :--------- |
| Cabbage x1   | $40   | Click 40 button once |
| Tomato x2    | $20   | Click 20 button twice or enter 2 |
| Carrot x1    | $40   | Click 40 button once |
| Apple x1     | $5    | Click 5 button once |

Total items: 5
Total purchase:	$125
Adjustment amount: 1
Payment: $200
Change: $74


## Project setup
This is a VueJs app with VueJs Bootstrap.  

1. Run following command to download all packages.
```
npm install
```
2. Compiles and hot-reloads for development. 
```
npm run serve
```
3. Compiles and minifies for production.
```
npm run build
```
4. Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
