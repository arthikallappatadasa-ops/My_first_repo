

import datetime

orders = []   # List to store all orders

def take_order():
    print("\n=== NEW ORDER ===")
    customer_name = input("Enter customer name: ")
    event_type = input("Enter event type (Wedding/Birthday/Other): ")
    plates = int(input("Enter number of plates: "))

    print("\nMenu:")
    print("1. Veg – ₹150 per plate")
    print("2. Non-Veg – ₹250 per plate")

    choice = int(input("Choose menu (1 or 2): "))

    if choice == 1:
        price = 150
        menu = "Veg"
    elif choice == 2:
        price = 250
        menu = "Non-Veg"
    else:
        print("Invalid choice!")
        return

    total = plates * price
    date = datetime.date.today()

    order = {
        "name": customer_name,
        "event": event_type,
        "menu": menu,
        "plates": plates,
        "price": price,
        "total": total,
        "date": str(date)
    }

    orders.append(order)
    save_order(order)

    print("\nOrder added successfully!")
    print("Total Amount: ₹", total)


def save_order(order):
    with open("orders.txt", "a") as file:
        file.write(str(order) + "\n")


def view_all_orders():
    print("\n=== ALL ORDERS ===")
    for order in orders:
        print(order)


def calculate_total_earnings():
    total_income = sum(order["total"] for order in orders)
    print("\nTotal Earnings: ₹", total_income)


def menu():
    while True:
        print("\n====== CATERING MANAGEMENT SYSTEM ======")
        print("1. Take New Order")
        print("2. View All Orders")
        print("3. Total Earnings")
        print("4. Exit")

        choice = int(input("Enter choice: "))

        if choice == 1:
            take_order()
        elif choice == 2:
            view_all_orders()
        elif choice == 3:
            calculate_total_earnings()
        elif choice == 4:
            print("Thank you! Exiting...")
            break
        else:
            print("Invalid option!")


menu()
