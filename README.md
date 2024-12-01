# kyb4188.github.io
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Order Ice Cream</title>
  <script type="module">
    // Firebase 설정
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.17.1/firebase-app.js";
    import { getDatabase, ref, push } from "https://www.gstatic.com/firebasejs/9.17.1/firebase-database.js";

    const firebaseConfig = {
      apiKey: "your-api-key",
      authDomain: "your-auth-domain",
      databaseURL: "your-database-url",
      projectId: "your-project-id",
      storageBucket: "your-storage-bucket",
      messagingSenderId: "your-messaging-sender-id",
      appId: "your-app-id"
    };

    const app = initializeApp(firebaseConfig);
    const database = getDatabase(app);

    // 주문 데이터 전송 함수
    async function submitOrder(event) {
      event.preventDefault();

      const flavor = document.getElementById('flavor').value;
      const quantity = document.getElementById('quantity').value;

      if (!flavor || !quantity) {
        alert('Please fill in all fields.');
        return;
      }

      const ordersRef = ref(database, 'orders');
      await push(ordersRef, { flavor, quantity, timestamp: Date.now() });

      alert('Order submitted successfully!');
      document.getElementById('orderForm').reset();
    }
  </script>
</head>
<body>
  <h1>Order Ice Cream</h1>
  <form id="orderForm" onsubmit="submitOrder(event)">
    <label for="flavor">Flavor:</label>
    <select id="flavor" name="flavor" required>
      <option value="vanilla">Vanilla</option>
      <option value="chocolate">Chocolate</option>
      <option value="strawberry">Strawberry</option>
    </select>
    <br>
    <label for="quantity">Quantity:</label>
    <input type="number" id="quantity" name="quantity" min="1" required>
    <br>
    <button type="submit">Submit Order</button>
  </form>
</body>
</html>
