📄 Swagger Upload & Auth Microservice

This is a simple Node.js + Express-based microservice that supports:

📝 User registration & login with JWT-based authentication
🔐 Role-based access control (user & admin)
📤 Admin-only Swagger file upload & validation (YAML/JSON)

It demonstrates how to build a secure REST API with file uploads, authentication, and role-based permissions.


🚀 Features
✅ User registration & login (email + password)
✅ Passwords hashed with bcrypt
✅ JWT token-based authentication with expiry
✅ Role-based access (user, admin) enforced through middleware
✅ Supports uploading Swagger specs either:

as pasted text (application/json or text/plain)

or as file upload (multipart/form-data)
✅ Validates uploaded Swagger as either valid JSON or valid YAML

🧰 Tech Stack & Libraries Used
Node.js (v21 tested) — Server-side runtime
Express.js — Routing & middleware framework
MongoDB + Mongoose — Database & ODM
bcrypt / bcryptjs — Secure password hashing
jsonwebtoken — JWT token generation & verification
dotenv — Environment variable management
multer — Handling file uploads
js-yaml — Parsing YAML files
cors — Cross-origin request support

📂 Project Structure
/controllers
    adminController.js      # Swagger upload handler
    authController.js       # User login & registration
/middleware
    authMiddleware.js       # JWT authentication
    roleMiddleware.js       # Admin-only check
/models
    User.js                  # User schema with pre-save hash
/routes
    adminRoutes.js           # /api/admin routes
    authRoutes.js            # /api/auth routes
app.js                       # Main server file

🛡️ Functions/Logic Highlighted
🔐 Authentication:
Registration: hashes password using bcrypt before saving

Login: verifies password with bcrypt.compare

Generates JWT with user ID and role in payload (using jsonwebtoken)

📝 Middleware:
protect: checks Authorization header for JWT, verifies it, and attaches user info to req
adminOnly: checks req.userRole and rejects if not admin

📄 Swagger Upload:

Accepts Swagger definition either:
via req.body.swaggerText
or via uploaded file using multer

Validates content:
First tries JSON.parse
If that fails, tries js-yaml.load
Responds with success/failure message accordingly

