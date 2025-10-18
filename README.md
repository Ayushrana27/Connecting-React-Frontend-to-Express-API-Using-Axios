🚀 React + Express Product App

A simple full-stack project combining Express.js (Backend) and React (Frontend) to display a list of products 📦 with their names and prices fetched from an API.
This project demonstrates how to connect a React app with an Express backend using Axios for API calls.

🧩 Project Structure
product-app/
├── backend/
│   ├── server.js
│   └── package.json
└── frontend/
    ├── src/
    │   ├── ProductList.jsx
    │   └── App.js
    └── package.json

⚙️ Backend Setup (Express.js)
📁 Navigate to backend folder
cd backend
npm init -y
npm install express cors

✨ Create server.js
const express = require('express');
const cors = require('cors');
const app = express();
const PORT = 5000;

app.use(cors());

const products = [
  { id: 1, name: 'RoadWare Car Perfume', price: 399 },
  { id: 2, name: 'RoadWare Seat Cover', price: 1299 },
  { id: 3, name: 'RoadWare Dashboard Polish', price: 499 },
];

app.get('/products', (req, res) => {
  res.json(products);
});

app.listen(PORT, () => console.log(`✅ Server running on http://localhost:${PORT}`));

▶️ Run backend
node server.js

⚛️ Frontend Setup (React.js)
📁 Navigate to frontend folder
cd frontend
npx create-react-app .
npm install axios

✨ Create src/ProductList.jsx
import React, { useEffect, useState } from 'react';
import axios from 'axios';

export default function ProductList() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    axios.get('http://localhost:5000/products')
      .then(res => {
        setProducts(res.data);
        setLoading(false);
      })
      .catch(() => {
        setError('⚠️ Failed to fetch products');
        setLoading(false);
      });
  }, []);

  if (loading) return <p style={{ textAlign: 'center' }}>⏳ Loading products...</p>;
  if (error) return <p style={{ color: 'red', textAlign: 'center' }}>{error}</p>;

  return (
    <div style={{
      display: 'grid',
      gap: '1rem',
      gridTemplateColumns: 'repeat(auto-fit, minmax(200px, 1fr))',
      padding: '20px'
    }}>
      {products.map(p => (
        <div key={p.id} style={{
          border: '1px solid #ccc',
          borderRadius: '10px',
          padding: '15px',
          boxShadow: '0 2px 5px rgba(0,0,0,0.1)',
          transition: '0.3s',
        }}>
          <h3>🛞 {p.name}</h3>
          <p>💰 Price: ₹{p.price}</p>
        </div>
      ))}
    </div>
  );
}

🧠 Update App.js
import React from 'react';
import ProductList from './ProductList';

function App() {
  return (
    <div>
      <h1 style={{ textAlign: 'center' }}>🛍️ RoadWare Product Store</h1>
      <ProductList />
    </div>
  );
}

export default App;

▶️ Run frontend
npm start

✅ Testing the App

Start backend:

node server.js


Start frontend:

npm start


Visit 👉 http://localhost:3000

You should see a list of RoadWare products fetched from your Express API 🎉

🧠 Features

🔗 Seamless API connection between React & Express

⚡ Axios for data fetching

⏳ Loading & error handling

💎 Clean, minimal UI

🧱 Modular code structure

🧰 Tech Stack
Layer	Technology
Frontend	React.js ⚛️
Backend	Express.js 🚀
API Calls	Axios 🌐
Styling	Inline + Simple Grid 💅
📸 Preview

🖼️ Coming Soon — integrate your screenshots here once the app runs locally!

💡 Author

👨‍💻 Ayush Rana
Founder of RoadWare — A Gen Z brand for car lovers 🚗💨
