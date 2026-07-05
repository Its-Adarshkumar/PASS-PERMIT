# Pass-Permit 🛂

**Pass-Permit** is a digital pass / permit management system built for a two-sided workflow: an **applicant (user) side** for requesting an entry/admit pass, and an **admin (HR) side** for reviewing, approving, and issuing that pass back to the user — complete with QR-code verification and a downloadable PDF pass.

The deployed demo is themed as an **Airports Authority Digital Pass Management System**, but the underlying flow (apply → review → approve → issue) generalizes to any organization that needs to vet and issue access passes (offices, events, restricted facilities, etc.).

🔗 **Live demo:** [pass-permit.onrender.com](https://pass-permit.onrender.com/home)
📦 **Repository:** [github.com/Its-Adarshkumar/PASS-PERMIT](https://github.com/Its-Adarshkumar/PASS-PERMIT)

> ⚠️ Note: the live demo is hosted on Render's free tier, so the first request after a period of inactivity may take 30–60 seconds to spin up.

---

## ✨ Features

### 👤 User side
- Sign up / log in with a secure, session-based authentication flow
- Fill out and submit a pass/permit application (personal details, purpose, supporting photo/document upload)
- Track the status of a submitted application (pending / approved / rejected)
- Once approved, receive the issued pass with an embedded **QR code** for verification
- Download the approved pass as a **PDF**

### 🛡️ Admin (HR) side
- Separate authenticated admin login
- View all incoming pass applications in a dashboard
- Inspect applicant details and uploaded documents/photos
- Approve or reject applications
- On approval, the system auto-generates a QR-coded pass and makes it available to the corresponding user

### ⚙️ Under the hood
- QR codes are generated per approved pass for quick, tamper-evident verification
- Passes are rendered to PDF (via headless Chrome/Puppeteer) for download and printing
- Uploaded images/documents are stored via Cloudinary
- Server-side validation on all form submissions

---

## 🧰 Tech Stack

| Layer            | Technology |
|-------------------|------------|
| Runtime           | Node.js |
| Web framework     | Express 5 |
| Templating        | EJS + `ejs-mate` (layouts/partials) |
| Database          | MongoDB with Mongoose (ODM) |
| Authentication    | Passport.js (`passport-local`, `passport-local-mongoose`) + `express-session` |
| Validation        | Joi |
| File uploads      | Multer + Cloudinary + Streamifier |
| PDF generation    | Puppeteer |
| QR code generation| `qrcode` |
| Flash messages    | connect-flash |
| Env config        | dotenv |

---

## 📁 Project Structure

```
PASS-PERMIT/
├── models/          # Mongoose schemas (User/HR, Pass, etc.)
├── pdf/             # Generated / template PDF assets for issued passes
├── public/          # Static assets (CSS, client-side JS, images)
├── uploads/         # Locally staged uploads before/around Cloudinary storage
├── utils/           # Helper/utility modules (e.g. error handling, wrappers)
├── views/           # EJS templates for user & admin(HR) pages
├── app.js           # Application entry point (Express app, routes, DB connection)
├── middleware.js     # Auth/role guards and shared middleware
├── schema.js         # Joi validation schemas
├── seedHR.js         # Script to seed an initial HR/admin account
├── seedPass.js        # Script to seed sample pass data
├── package.json
└── .gitignore
```

---

## 🚀 Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (v18+ recommended)
- A [MongoDB](https://www.mongodb.com/) database (local or Atlas)
- A [Cloudinary](https://cloudinary.com/) account (for file/image uploads)

### 1. Clone the repository
```bash
git clone https://github.com/Its-Adarshkumar/PASS-PERMIT.git
cd PASS-PERMIT
```

### 2. Install dependencies
```bash
npm install
```

### 3. Configure environment variables
Create a `.env` file in the project root with the following (adjust names to match what `app.js` expects):

```env
MONGO_URI=your_mongodb_connection_string
SESSION_SECRET=your_session_secret
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret
PORT=3000
```

### 4. (Optional) Seed initial data
To create a default HR/admin account and/or sample pass data:
```bash
node seedHR.js
node seedPass.js
```

### 5. Run the app
```bash
npm start
```

The app will be available at `http://localhost:3000` (or your configured `PORT`).

---

## 🔄 How It Works

1. **User applies** — A user creates an account, logs in, and submits a pass application with the required details and documents.
2. **HR reviews** — An HR/admin user logs into the admin dashboard and reviews pending applications.
3. **HR approves/rejects** — On approval, a unique pass is generated with an embedded QR code (and made available as a PDF); on rejection, the user is notified of the status.
4. **User receives the pass** — The user sees the updated status on their dashboard and can download/print their approved digital pass, which can be verified via its QR code.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome. Feel free to check the [issues page](https://github.com/Its-Adarshkumar/PASS-PERMIT/issues) or open a pull request.

## 📄 License

This project is licensed under the **ISC License**.

## 👤 Author

**Adarsh Kumar** — [GitHub](https://github.com/Its-Adarshkumar)