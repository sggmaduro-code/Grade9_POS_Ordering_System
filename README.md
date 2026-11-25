# Grade9_POS_Ordering_System
# for our practical 
# Point-of-Sale (POS) Ordering System
# Developers: Maduro, Fesalbon



# A. PRODUCT MENU

products = {
    1: {"name": "Burger", "price": 50.00},
    2: {"name": "Fries", "price": 35.00},
    3: {"name": "Soft Drink", "price": 25.00}
}

def display_menu():
    print("=" * 40)
    print("           PRODUCT MENU")
    print("=" * 40)
    print(f"{'No.':<5} {'Product':<15} {'Price':>10}")
    print("-" * 40)
    for key, item in products.items():
        print(f"{key:<5} {item['name']:<15} P{item['price']:>8.2f}")
    print("=" * 40)

# B. CUSTOMER ORDER

def take_order():
    order_list = []
    while True:
        try:
            choice = int(input("\nEnter the product number to order (1-3): "))
            if choice not in products:
                print("Invalid product number. Please try again.")
                continue
            
            quantity = int(input(f"Enter quantity for {products[choice]['name']}: "))
            if quantity <= 0:
                print("Quantity must be at least 1.")
                continue
            
            subtotal = products[choice]['price'] * quantity
            order_list.append({
                "name": products[choice]['name'],
                "price": products[choice]['price'],
                "quantity": quantity,
                "subtotal": subtotal
            })
            print(f"Added: {quantity}x {products[choice]['name']} - P{subtotal:.2f}")
            
            more = input("\nOrder another item? (y/n): ").lower().strip()
            if more != 'y':
                break
        
        except ValueError:
            print("Please enter a valid number.")
    
    return order_list


# C. RECEIPT GENERATION

def display_receipt(order_list):
    print("\n" + "=" * 50)
    print("                RECEIPT")
    print("=" * 50)
    print(f"{'Item':<15} {'Qty':>6} {'Price':>10} {'Subtotal':>12}")
    print("-" * 50)
    
    grand_total = 0
    for item in order_list:
        print(f"{item['name']:<15} {item['quantity']:>6} P{item['price']:>8.2f} P{item['subtotal']:>10.2f}")
        grand_total += item['subtotal']
    
    print("-" * 50)
    print(f"TOTAL AMOUNT DUE: P{grand_total:>30.2f}")
    print("=" * 50)
    print(" thank you for your purchase!")
    print("=" * 50)

# D. MAIN PROGRAM

if __name__ == "__main__":
    print("\nWelcome to the Store POS System!")
    display_menu()
    my_order = take_order()
    if my_order:
        display_receipt(my_order)
    else:
        print("\nNo items were ordered. thanks")
