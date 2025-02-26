# Reto_8
- The menu once again....(I am running out of ideas). Well the task is quite easy, take the Menu code from Reto 3 and implement a new Class that creates and iterable with all the items in an order, it should allow looping and contain all item attributes.

```python
class MenuItem:
    def __init__(self, name, price):
        self.name = name
        self.price = price

    def calculate_price(self):
        return self.price

    def __str__(self):
        return f"{self.name}: ${self.price:.2f}"


class Beverage(MenuItem):
    def __init__(self, name, price, size):
        super().__init__(name, price)
        self.size = size

    def __str__(self):
        return f"{self.name} ({self.size}): ${self.price:.2f}"


class Appetizer(MenuItem):
    def __init__(self, name, price, spicy=False):
        super().__init__(name, price)
        self.spicy = spicy

    def __str__(self):
        spice = "Spicy" if self.spicy else "Non-Spicy"
        return f"{self.name} ({spice}): ${self.price:.2f}"


class MainCourse(MenuItem):
    def __init__(self, name, price, vegetarian=False):
        super().__init__(name, price)
        self.vegetarian = vegetarian

    def __str__(self):
        type_of_dish = "Vegetarian" if self.vegetarian else "Non-Vegetarian"
        return f"{self.name} ({type_of_dish}): ${self.price:.2f}"


class OrderIterator:
    def __init__(self, items):
        self._items = items
        self._index = 0

    def __iter__(self):
        return self

    def __next__(self):
        if self._index < len(self._items):
            item = self._items[self._index]
            self._index += 1
            return item
        raise StopIteration


class Order:
    def __init__(self):
        self.items = []

    def add_item(self, menu_item):
        self.items.append(menu_item)

    def calculate_total(self):
        return sum(item.calculate_price() for item in self.items)

    def apply_discount(self):
        total = self.calculate_total()
        if len(self.items) > 5:
            total *= 0.10
        return total

    def print_receipt(self):
        print("Order Receipt:")
        for item in self.items:
            print(f"- {item}")
        print(f"\nSubtotal: ${self.calculate_total():.2f}")
        Subtotal = self.calculate_total()
        discounted_total = self.apply_discount()
        if discounted_total != Subtotal:
            print(f"Discounted Total: ${discounted_total:.2f}")
            Total = self.calculate_total() - discounted_total
            print(f"Total: $ {Total:.2f}")
        else:
            print(f"Total: $ {Subtotal:.2f}")

    def __iter__(self):
        return OrderIterator(self.items)

# Prueba de la implementación
if __name__ == "__main__":
    order = Order()
    order.add_item(Beverage("Coke", 2.0, "small"))
    order.add_item(Beverage("Tamarindo", 3.0, "medium"))
    order.add_item(Beverage("Jamaica", 2.5, "Large"))
    order.add_item(Appetizer("Tacos de al pastor", 3.0, True))
    order.add_item(Appetizer("Flauta", 6.5, False))
    order.add_item(Appetizer("Tamal", 3.5, False))
    order.add_item(Appetizer("Elote", 4.5, False))
    order.add_item(MainCourse("Veggie Burrito", 8.0, True))
    order.add_item(MainCourse("Enchilada", 12.0, True))
    order.add_item(MainCourse("Tomato Soup", 12.0, True))

    # Imprimir el recibo
    order.print_receipt()

    # Recibo iterando
    print("\nOrden iterando:")
    for item in order:
        print(item)

```
