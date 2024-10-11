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
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wrong Delivery Resolver</title>
    <script defer src="script.js"></script>
</head>
<body>
    <h1>Wrong Delivery Resolver</h1>
    <form id="delivery-form">
        <label for="order-id">Order ID:</label>
        <input type="text" id="order-id" name="order-id" required>
        <button type="submit">Check Delivery</button>
    </form>
    <div id="result"></div>
</body>
</html>
import requests

def get_openai_response(prompt, api_key):
    endpoint = "https://api.openai.com/v1/engines/davinci-codex/completions"
    headers = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {api_key}"
    }

    data = {
        "prompt": prompt,
        "max_tokens": 150,
        "n": 1,
        "stop": None,
        "temperature": 0.5
    }

    response = requests.post(endpoint, headers=headers, json=data)
    if response.status_code == 200:
        result = response.json()
        return result["choices"][0]["text"].strip()
    else:
        return "An error occurred while processing the request."
try:
    # Existing code logic
    response = requests.post(endpoint, headers=headers, json=data)
    response.raise_for_status()  # Check for HTTP errors
except requests.exceptions.RequestException as e:
    return f"An error occurred: {e}"
from flask_sqlalchemy import SQLAlchemy

app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///guardivery.db'
db = SQLAlchemy(app)

class Order(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    order_id = db.Column(db.String(50), unique=True, nullable=False)
    items = db.Column(db.PickleType, nullable=False)

