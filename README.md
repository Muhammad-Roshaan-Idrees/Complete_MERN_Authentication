# Complete MERN Authentication

A full-stack MERN (MongoDB, Express, React, Node.js) authentication system with email verification, OTP verification, password reset, and SMS features.

## Features

- User Registration with Email/OTP Verification
- User Login with JWT Authentication
- Password Reset via Email
- SMS Verification (Twilio)
- Protected Routes
- Secure HTTP-only Cookies
- Auto-removal of Unverified Accounts

## Tech Stack

**Frontend:**
- React 18
- Vite
- React Router DOM
- Axios
- React Hook Form
- React Toastify

**Backend:**
- Node.js
- Express
- MongoDB with Mongoose
- JWT for Authentication
- Nodemailer for Email
- Twilio for SMS
- Bcrypt for Password Hashing
- Node-Cron for Scheduled Tasks

## Prerequisites

Before running this project, make sure you have:

- Node.js (v14 or higher)
- npm or yarn
- MongoDB Atlas account (free tier) OR MongoDB installed locally
- Gmail account (for email features)
- Twilio account (optional, for SMS features)

## Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Zeeshu911/Complete_MERN_Authentication.git
cd Complete_MERN_Authentication
```

### 2. Install Dependencies

**Install Backend Dependencies:**
```bash
cd server
npm install
```

**Install Frontend Dependencies:**
```bash
cd ../client
npm install
```

### 3. Configure Environment Variables

Navigate to the `server` folder and create a `config.env` file:

```bash
cd server
```

Copy the contents from `.env.example` and fill in your actual credentials:

#### Required Configuration:

**MongoDB Setup:**
- **Option 1 (Recommended):** MongoDB Atlas (Free)
  1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register)
  2. Create a free account and cluster
  3. Click "Connect" → "Connect your application"
  4. Copy the connection string
  5. Replace `<password>` with your database password
  
- **Option 2:** Local MongoDB
  ```
  MONGO_URI=mongodb://localhost:27017/mern_authentication
  ```

**Email Setup (Gmail):**
1. Enable 2-Step Verification on your Google Account
2. Generate an App Password: [Google App Passwords](https://myaccount.google.com/apppasswords)
3. Use this 16-character password in `SMTP_PASSWORD`

**JWT Secret:**
- Generate a random string for `JWT_SECRET_KEY` (can be any random string)

**Twilio Setup (Optional - for SMS features):**
1. Sign up at [Twilio](https://www.twilio.com/)
2. Get your Account SID, Auth Token, and Phone Number
3. Add them to the config file

### 4. Example config.env File

```env
PORT=4000
FRONTEND_URL=http://localhost:5173
MONGO_URI=mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/mern_auth?retryWrites=true&w=majority
JWT_EXPIRE=7d
JWT_SECRET_KEY=your_random_secret_key_here_make_it_long_and_secure
COOKIE_EXPIRE=7
SMTP_SERVICE=gmail
SMTP_MAIL=youremail@gmail.com
SMTP_PASSWORD=your_16_char_app_password
SMTP_HOST=smtp.gmail.com
SMTP_PORT=465
TWILIO_SID=ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
TWILIO_PHONE_NUMBER=+1234567890
TWILIO_AUTH_TOKEN=your_auth_token_here
```

### 5. Run the Application

**Start the Backend Server:**
```bash
cd server
npm start
```

The server will run on `http://localhost:4000`

**Start the Frontend (in a new terminal):**
```bash
cd client
npm run dev
```

The client will run on `http://localhost:5173`

## Project Structure

```
Complete_MERN_Authentication/
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/    # React components
│   │   ├── pages/         # Page components
│   │   ├── styles/        # CSS files
│   │   └── App.jsx        # Main App component
│   └── package.json
│
└── server/                # Node.js backend
    ├── controllers/       # Request handlers
    ├── models/           # Mongoose models
    ├── routes/           # API routes
    ├── middlewares/      # Custom middlewares
    ├── utils/            # Utility functions
    ├── automation/       # Cron jobs
    ├── database/         # DB connection
    └── package.json
```

## API Endpoints

### Authentication Routes

- `POST /api/v1/user/register` - Register new user
- `POST /api/v1/user/verify` - Verify email/OTP
- `POST /api/v1/user/login` - User login
- `GET /api/v1/user/logout` - User logout
- `GET /api/v1/user/me` - Get current user
- `POST /api/v1/user/forgot-password` - Request password reset
- `POST /api/v1/user/reset-password/:token` - Reset password

## Features Explained

### Email Verification
Users receive an OTP via email upon registration that must be verified before account activation.

### Password Reset
Users can request a password reset link via email. The link expires after a set time.

### Auto-cleanup
Unverified accounts are automatically deleted after 24 hours using a cron job.

### JWT Authentication
Secure token-based authentication with HTTP-only cookies.

## Troubleshooting

**MongoDB Connection Error:**
- Check your connection string format
- Ensure your IP is whitelisted in MongoDB Atlas
- Verify database user credentials

**Email Not Sending:**
- Confirm Gmail App Password is correct
- Enable 2-Step Verification on Google Account
- Check if "Less secure app access" is handled via App Passwords

**Port Already in Use:**
- Change the PORT in config.env
- Or kill the process using the port

## Security Notes

- Never commit `config.env` to version control (it's in `.gitignore`)
- Use strong JWT secret keys
- Keep your MongoDB credentials secure
- Use environment variables for all sensitive data

## Contributing

Feel free to submit issues and pull requests!

## License

MIT License

## Author

Zeeshu911

## Support

For issues and questions, please open an issue on GitHub.
