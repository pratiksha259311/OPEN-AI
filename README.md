# Define the Order and Delivery classes
class Order:
    def __init__(self, order_id, items):
        self.order_id = order_id
        self.items = items

class Delivery:
    def __init__(self, delivery_id, items):
        self.delivery_id = delivery_id
        self.items = items

# Function to check for wrong delivery
def check_delivery(order, delivery):
    if order.order_id != delivery.delivery_id:
        return "Delivery ID does not match Order ID."

    for item in order.items:
        if item not in delivery.items:
            return f"Item '{item}' is missing in the delivery."

    for item in delivery.items:
        if item not in order.items:
            return f"Extra item '{item}' found in the delivery."

    return "Delivery matches the order."

# Example usage
order = Order(order_id="12345", items=["laptop", "mouse", "keyboard"])
delivery = Delivery(delivery_id="12345", items=["laptop", "mouse", "keyboard"])

result = check_delivery(order, delivery)
print(result)
