# task2
class Product:
    def __init__(self, product_id, name, price):
        self.product_id = product_id
        self.name = name
        self.price = price

class Cart:
    def __init__(self):
        self.items = {}

    def add_to_cart(self, product, quantity):
        if product.product_id in self.items:
            self.items[product.product_id]['quantity'] += quantity
        else:
            self.items[product.product_id] = {'product': product, 'quantity': quantity}

    def view_cart(self):
        if not self.items:
            print("Your cart is empty.")
            return

        print("\nItems in your cart:")
        for item in self.items.values():
            product = item['product']
            quantity = item['quantity']
            print(f"{product.name} - ${product.price} x {quantity} = ${product.price * quantity}")

    def calculate_total(self):
        total = sum(item['product'].price * item['quantity'] for item in self.items.values())
        return total

    def checkout(self):
        if not self.items:
            print("Your cart is empty. Add items before checkout.")
            return

        total = self.calculate_total()
        print(f"\nYour total is: ${total}")
        confirm = input("Do you want to proceed to checkout? (yes/no): ").strip().lower()
        if confirm == 'yes':
            print("Checkout successful! Thank you for your purchase.")
            self.items.clear()
        else:
            print("Checkout canceled.")

class ECommerce:
    def __init__(self):
        self.products = []
        self.cart = Cart()

    def add_product(self, product):
        self.products.append(product)

    def show_products(self):
        if not self.products:
            print("No products available.")
            return

        print("\nAvailable Products:")
        for product in self.products:
            print(f"{product.product_id}. {product.name} - ${product.price}")

    def run(self):
        while True:
            print("\nWelcome to the E-Commerce Platform!")
            print("1. View Products")
            print("2. Add to Cart")
            print("3. View Cart")
            print("4. Checkout")
            print("5. Exit")

            choice = input("Enter your choice: ").strip()

            if choice == '1':
                self.show_products()
            elif choice == '2':
                self.show_products()
                product_id = input("Enter the product ID to add to cart: ").strip()
                quantity = int(input("Enter the quantity: ").strip())

                product = next((p for p in self.products if str(p.product_id) == product_id), None)
                if product:
                    self.cart.add_to_cart(product, quantity)
                    print(f"Added {quantity} x {product.name} to cart.")
                else:
                    print("Invalid product ID.")
            elif choice == '3':
                self.cart.view_cart()
            elif choice == '4':
                self.cart.checkout()
            elif choice == '5':
                print("Thank you for visiting! Goodbye!")
                break
            else:
                print("Invalid choice. Please try again.")
