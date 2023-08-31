# E-commerce-Website
const express = require('express');
const app = express();
const bodyParser = require('body-parser');

// const PORT = process.env.PORT || 3000;

app.use(bodyParser.json());
// Data to simulate a database
const invoices = [];

// API to create an invoice
app.post('/invoices', (req, res) => {
  const { customerName, amount } = req.body;
  const invoice = {
    id: invoices.length + 1,
    customerName,
    amount,
    status: 'confirmed',
  };
  invoices.push(invoice);
  res.status(201).json(invoice);
});

// API to get all invoices
app.get('/invoices', (req, res) => {
  res.json(invoices);
});

// Create an account for the user
app.post('/account', (req, res) => {
  // Implement create account for the user functionality
  res.json({ message: 'Account created successfully' });
});

// Fetch all products and services information with their prices
app.get('/products', (req, res) => {
  // Implement fetch products functionality
  res.json({ products: [] });
});

// Add a product to the cart
app.post('/cart', (req, res) => {
  // Implement add to cart functionality
  res.json({ message: 'Item added to cart successfully' });
});

// Remove a product from the cart
app.delete('/cart/:itemId', (req, res) => {
  const itemId = req.params.itemId;
  // Implement remove from cart functionality
  res.json({ message: `Item ${itemId} removed from cart successfully` });
});

// View the total bill
app.get('/bill', (req, res) => {
  // Implement view total bill functionality
  res.json({ bill: {} });
});

// Confirm the order
app.post('/order', (req, res) => {

  // Implement confirm order functionality
  res.json({ message: 'Order confirmed successfully' });
});

const calculateProductTax = (price) => {
  if (price > 1000 && price <= 5000) {
    return price * 0.12;
  } else if (price > 5000) {
    return price * 0.18;
  } else {
    return 0;
  }
};

const calculateServiceTax = (price) => {
  if (price > 1000 && price <= 8000) {
    return price * 0.10;
  } else if (price > 8000) {
    return price * 0.15;
  } else {
    return 0;
  }
};

// API endpoint for billing products
app.post('/bill-product', (req, res) => {
  const { productName, price } = req.body;
  const productTax = calculateProductTax(price);
  const totalAmount = price + productTax;

  res.json({
    productName,
    price,
    productTax,
    totalAmount,
  });
});

// API endpoint for billing services
app.post('/bill-service', (req, res) => {
  const { serviceName, price } = req.body;
  const serviceTax = calculateServiceTax(price);
  const totalAmount = price + serviceTax;

  res.json({
    serviceName,
    price,
    serviceTax,
    totalAmount,
  });
});

// Start the server
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});

