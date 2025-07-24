# Budget Tracker - Multi-User Setup Guide

## 🚀 Quick Start

### Prerequisites
- Node.js (version 14 or higher)
- npm (comes with Node.js)

### 1. Project Setup

Create a new directory and set up the project:

```bash
mkdir budget-tracker-app
cd budget-tracker-app
```

### 2. Initialize the Project

Create the `package.json` file with the provided configuration, then install dependencies:

```bash
npm install
```

### 3. Project Structure

Your project should have this structure:

```
budget-tracker-app/
├── server.js              # Backend server
├── package.json           # Dependencies and scripts
├── public/
│   └── index.html        # Frontend HTML file
└── README.md             # This file
```

### 4. Create the Files

1. **Create `server.js`** - Copy the Node.js backend code
2. **Create `public/` directory** - `mkdir public`
3. **Create `public/index.html`** - Copy the updated frontend code

### 5. Environment Variables (Optional)

Create a `.env` file for production:

```bash
PORT=3000
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
```

### 6. Run the Application

For development:
```bash
npm run dev
```

For production:
```bash
npm start
```

The app will be available at: `http://localhost:3000`

---

## 🔧 Features

### Multi-User Support
- **User Registration**: Create new accounts with email/password
- **User Authentication**: Secure login with JWT tokens
- **Session Management**: Automatic token validation and logout
- **User Isolation**: Each user sees only their own transactions

### Budget Management
- **Add Transactions**: Income and expense tracking
- **Categories**: Organize transactions by type (Food, Transport, etc.)
- **Real-time Summary**: Automatic calculation of income, expenses, and balance
- **Delete Transactions**: Remove unwanted entries with smooth animations

### Security Features
- **Password Hashing**: Secure password storage with bcrypt
- **JWT Authentication**: Stateless authentication tokens
- **Protected Routes**: API endpoints require valid authentication
- **Input Validation**: Server-side validation for all data

---

## 🎯 API Endpoints

### Authentication
- `POST /api/register` - Create new user account
- `POST /api/login` - User login
- `GET /api/profile` - Get user profile (requires auth)

### Transactions
- `GET /api/transactions` - Get user's transactions (requires auth)
- `POST /api/transactions` - Add new transaction (requires auth)
- `DELETE /api/transactions/:id` - Delete transaction (requires auth)
- `GET /api/summary` - Get financial summary (requires auth)

---

## 🔒 Security Considerations

### For Production Deployment:

1. **Change JWT Secret**: Use a strong, unique secret key
2. **Use HTTPS**: Always use SSL certificates in production
3. **Database**: Replace in-memory storage with a real database (MongoDB, PostgreSQL, etc.)
4. **Rate Limiting**: Add rate limiting to prevent abuse
5. **Input Sanitization**: Add additional input validation and sanitization
6. **CORS Configuration**: Configure CORS for your specific domain

### Example Production Enhancements:

```javascript
// Add to server.js for production
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // limit each IP to 100 requests per windowMs
});

app.use('/api', limiter);
```

---

## 📦 Database Integration

To add a real database (MongoDB example):

```bash
npm install mongoose
```

```javascript
// Add to server.js
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/budget-tracker');

// User Schema
const userSchema = new mongoose.Schema({
  email: { type: String, unique: true, required: true },
  password: { type: String, required: true },
  name: { type: String, required: true },
  createdAt: { type: Date, default: Date.now }
});

// Transaction Schema
const transactionSchema = new mongoose.Schema({
  userId: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true },
  description: { type: String, required: true },
  amount: { type: Number, required: true },
  type: { type: String, enum: ['income', 'expense'], required: true },
  category: { type: String, required: true },
  date: { type: Date, default: Date.now }
});

const User = mongoose.model('User', userSchema);
const Transaction = mongoose.model('Transaction', transactionSchema);
```

---

## 🚀 Deployment Options

### Heroku
```bash
# Add Procfile
echo "web: node server.js" > Procfile

# Deploy
git init
git add .
git commit -m "Initial commit"
heroku create your-budget-app
git push heroku main
```

### DigitalOcean/AWS/Other VPS
1. Upload files to server
2. Install Node.js and npm
3. Run `npm install`
4. Use PM2 for process management:
   ```bash
   npm install -g pm2
   pm2 start server.js --name budget-app
   pm2 startup
   pm2 save
   ```

---

## 🎨 Customization

The app uses modern CSS with:
- **Gradient backgrounds** and **glassmorphism effects**
- **Smooth animations** and **hover interactions**
- **Responsive design** for mobile and desktop
- **Dark/light theme support** (can be extended)

Feel free to customize colors, fonts, and animations in the CSS section of `public/index.html`.

---

## 🐛 Troubleshooting

### Common Issues:

1. **Port already in use**: Change the PORT in package.json or environment
2. **CORS errors**: Add your frontend domain to CORS configuration
3. **Token expired**: Tokens expire after 24 hours, users need to log in again
4. **Database connection**: Ensure your database is running if using external DB

### Development Tips:

- Use `npm run dev` with nodemon for automatic restarts
- Check browser console for frontend errors
- Use Postman or similar tools to test API endpoints
- Enable Node.js debugging: `DEBUG=* npm run dev`

---

## 📄 License

MIT License - Feel free to use this project for personal or commercial purposes.# budget-tracker
# budget-tracker
# budget-tracker
