// edirector34 - index.js
// A simple backend server to redirect short paths to full profile links

const express = require('express');
const morgan = require('morgan');
const cors = require('cors');
const helmet = require('helmet');

const app = express();
const PORT = process.env.PORT || 3000;

// --- Middleware setup ---
app.use(morgan('dev'));       // Logging
app.use(cors());              // Allow cross-origin requests
app.use(helmet());            // Basic security headers
app.use(express.json());      // Parse JSON bodies

// --- Routes ---
// Root route
app.get('/', (req, res) => {
  res.send(`
    <h1>Redirector34 Server</h1>
    <p>Use <a href="/34">/34</a> to go to your profile.</p>
  `);
});

// Redirect route for number 34
app.get('/34', (req, res) => {
  res.redirect('https://app.ethos.network/profile/x/Bavariaade');
});

// Example: if you want to add more numbers later
app.get('/35', (req, res) => {
  res.redirect('https://example.com/some-other-link');
});

// 404 handler
app.use((req, res) => {
  res.status(404).json({
    error: true,
    message: 'Route not found'
  });
});

// --- Start server ---
app.listen(PORT, () => {
  console.log(`🚀 Redirector34 is running on http://localhost:${PORT}`);
});
