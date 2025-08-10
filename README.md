<!DOCTYPE html>
<html>
<head>
    <title>Biryani Order System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 30px;
            background-color: #fff8e1;
        }
        h1 {
            color: #d35400;
        }
        label, select, input, textarea {
            font-size: 16px;
            margin: 8px 0;
            display: block;
        }
        input, select, textarea {
            padding: 6px;
            width: 300px;
            max-width: 100%;
            box-sizing: border-box;
        }
        textarea {
            resize: vertical;
            height: 80px;
        }
        button {
            background-color: #d35400;
            color: white;
            padding: 10px 20px;
            border: none;
            cursor: pointer;
            font-size: 16px;
            border-radius: 4px;
            margin-top: 15px;
        }
        button:hover {
            background-color: #e67e22;
        }
        #result {
            margin-top: 25px;
            font-weight: bold;
            font-size: 18px;
            color: #2c3e50;
            white-space: pre-wrap;
        }
    </style>
</head>
<body>

    <h1>Biryani Order System</h1>

    <label for="biryani">Choose your Biryani:</label>
    <select id="biryani">
        <option value="Chicken Biryani" data-price="150">Chicken Biryani - ₹150</option>
        <option value="Mutton Biryani" data-price="200">Mutton Biryani - ₹200</option>
        <option value="Veg Biryani" data-price="100">Veg Biryani - ₹100</option>
        <option value="Egg Biryani" data-price="120">Egg Biryani - ₹120</option>
    </select>

    <label for="quantity">Quantity:</label>
    <input type="number" id="quantity" value="1" min="1">

    <label for="address">Delivery Address:</label>
    <textarea id="address" placeholder="Enter your delivery address here..."></textarea>

    <label for="payment">Payment Method:</label>
    <select id="payment">
        <option value="">-- Select Payment Method --</option>
        <option value="Cash on Delivery">Cash on Delivery</option>
        <option value="Online Payment">Online Payment</option>
    </select>

    <button onclick="placeOrder()">Place Order</button>

    <div id="result"></div>

    <script>
        function placeOrder() {
            const biryaniSelect = document.getElementById('biryani');
            const selectedOption = biryaniSelect.options[biryaniSelect.selectedIndex];
            const biryaniName = selectedOption.value;
            const price = Number(selectedOption.getAttribute('data-price'));
            const quantity = Number(document.getElementById('quantity').value);
            const address = document.getElementById('address').value.trim();
            const paymentMethod = document.getElementById('payment').value;

            if (quantity < 1 || isNaN(quantity)) {
                document.getElementById('result').textContent = "Please enter a valid quantity.";
                return;
            }
            if (address.length === 0) {
                document.getElementById('result').textContent = "Please enter your delivery address.";
                return;
            }
            if (paymentMethod === "") {
                document.getElementById('result').textContent = "Please select a payment method.";
                return;
            }

            const total = price * quantity;

            let paymentNote = "";
            if (paymentMethod === "Online Payment") {
                paymentNote = "\n(Note: Online payment processing is not implemented in this demo.)";
            }

            document.getElementById('result').textContent =
                `Order Summary:\n` +
                `- ${quantity} x ${biryaniName} (₹${price} each)\n` +
                `- Total Price: ₹${total}\n` +
                `- Delivery Address: ${address}\n` +
                `- Payment Method: ${paymentMethod}${paymentNote}\n\n` +
                `Thank you for your order!`;
        }
    </script>

</body>
</html>
