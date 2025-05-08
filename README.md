class CafeSystem:
    def __init__(self):
        self.menu = {
            "Coffee": 2.5,
            "Tea": 2.0,
            "Sandwich": 5.0,
            "Cake": 4.0
        }
        self.inventory = {
            "Coffee": 50,
            "Tea": 50,
            "Sandwich": 30,
            "Cake": 20
        }
        self.orders = []

    def display_menu(self):
        print("\n--- Menu ---")
        for item, price in self.menu.items():
            print(f"{item}: ${price:.2f}")

    def take_order(self):
        order = {}
        while True:
            self.display_menu()
            item = input("Enter item name (or 'done' to finish): ").title()
            if item.lower() == 'done':
                break
            if item in self.menu:
                quantity = int(input(f"How many {item}s? "))
                if self.inventory[item] >= quantity:
                    order[item] = quantity
                else:
                    print(f"Sorry, only {self.inventory[item]} {item}s left.")
            else:
                print("Item not on the menu.")
        if order:
            self.orders.append(order)
            self.update_inventory(order)
            self.generate_bill(order)

    def update_inventory(self, order):
        for item, qty in order.items():
            self.inventory[item] -= qty

    def generate_bill(self, order):
        print("\n--- Bill ---")
        total = 0
        for item, qty in order.items():
            price = self.menu[item] * qty
            print(f"{item} x{qty} - ${price:.2f}")
            total += price
        print(f"Total: ${total:.2f}")

    def run(self):
        print("Welcome to the Cafe!")
        while True:
            choice = input("\n1. Take Order\n2. Exit\nChoose an option: ")
            if choice == '1':
                self.take_order()
            elif choice == '2':
                print("Goodbye!")
                break
            else:
                print("Invalid option. Try again.")

if __name__ == "__main__":
    cafe = CafeSystem()
    cafe.run()
