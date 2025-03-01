SafetyNet is a web application designed to enhance personal safety by enabling users to register, authenticate, and manage complaints efficiently. The platform provides tools for both department officials and civilians to track and handle safety-related incidents.

Features
User Registration & Authentication: Secure sign-up and login for both civilians and department officials.
Complaint Management:
For Departments: View complaints, update statuses, and send emergency notifications.
For Civilians: Raise and track complaints.
Emergency Email Notifications: Departments can send urgent emails using Resend.
Tech Stack
Backend: Node.js, Express.js
Database: MongoDB
Frontend: React.js (if applicable)
Authentication: JWT (JSON Web Token)
File Uploads: Multer middleware
Email Service: Resend
Installation
Prerequisites
Node.js (v16+ recommended)
MongoDB (local or cloud, e.g., MongoDB Atlas)
npm or yarn package manager
Setup
Clone the repository:

bash
Copy
Edit
git clone https://github.com/Dyuloka/safetyNet.git
cd safetyNet
Install dependencies:

bash
Copy
Edit
npm install
Configure environment variables:
Create a .env file in the root directory and add the following:

env
Copy
Edit
PORT=8000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
RESEND_API_KEY=your_resend_api_key
SENDER_EMAIL=your_verified_sender_email
Replace placeholders with actual values.

Start the server:

bash
Copy
Edit
npm start
API Endpoints
Department Routes
POST /department/register – Register a new department.
POST /department/login – Authenticate and retrieve a JWT token.
POST /department/logout – Log out a department user.
POST /department/refresh-token – Refresh JWT token.
PATCH /department/change-password – Change password (requires authentication).
GET /department/current-user – Retrieve department details (requires authentication).
PATCH /department/update-account – Update department account (requires authentication).
POST /department/profile/emergency-email – Send emergency email using Resend (requires authentication).
Civilian Routes
POST /users/register – Register a new civilian user.
POST /users/login – Authenticate and retrieve a JWT token.
POST /users/logout – Log out a civilian user.
POST /users/refresh-token – Refresh JWT token.
PATCH /users/change-password – Change password (requires authentication).
GET /users/current-user – Retrieve civilian details (requires authentication).
POST /users/profile/raise-complaint – Submit a complaint with optional image upload (requires authentication).
GET /users/profile/get-complaints – Retrieve complaints submitted by the civilian user.
Resend Email Integration
The application uses Resend for sending emergency emails. To set it up:

Sign Up at Resend and get an API key.
Verify a sender email in Resend's dashboard.
Add the API key & sender email to the .env file:
env
Copy
Edit
RESEND_API_KEY=your_resend_api_key
SENDER_EMAIL=your_verified_sender_email
Send an email using Resend in your code:
javascript
Copy
Edit
const Resend = require('resend');
const resend = new Resend(process.env.RESEND_API_KEY);

async function sendEmergencyEmail(to, subject, message) {
  await resend.emails.send({
    from: process.env.SENDER_EMAIL,
    to,
    subject,
    html: `<p>${message}</p>`,
  });
}
Troubleshooting
Cannot POST /users/register
Ensure the user routes are correctly mounted in your server.js or app.js:
javascript
Copy
Edit
app.use("/users", userRoutes);
Request body is undefined
Verify that Express JSON middleware is included:
javascript
Copy
Edit
app.use(express.json());
Database connection issues
Ensure MongoDB is running and MONGO_URI in .env is correct.
