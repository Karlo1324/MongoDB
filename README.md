## Reflection

 1. Why is password hashing important, and why should plain-text passwords never be stored in a database?

Storing plain-text passwords exposes users to severe security risks if a database breach occurs. Passwords hashed with algorithms like **bcrypt** use a one-way mathematical function along with a unique salt. This ensures that even if attackers gain full database access, they cannot reverse the hashes into the original passwords or perform effective rainbow table attacks.

2. How does JSON Web Token (JWT) authentication work in a REST API?

JWT provides a stateless authentication mechanism. Upon successful login, the server generates a signed token containing user claims (like the user ID) and sends it to the client. For subsequent protected requests, the client sends this token in the `Authorization` header (`Bearer <token>`). The server verifies the token's cryptographic signature using a secret key, without needing to query the database on every request.

3. What is the role of middleware in Express.js routes?

Middleware functions execute sequentially during the request-response lifecycle. In protected routes, middleware like `requireAuth` intercepts incoming requests to verify the presence and validity of the JWT before allowing execution to proceed to the main route handler via `next()`. If verification fails, it halts execution and returns an unauthorized status (e.g., `401 Unauthorized`).
4. What is the difference between `401 Unauthorized` and `403 Forbidden` HTTP status codes?

- **`401 Unauthorized`**: Authentication is missing or invalid (e.g., no token provided, invalid token format, or expired token).
- **`403 Forbidden`**: The server recognizes the authenticated user, but that user lacks the required permissions or roles to access the requested resource.

5. Why do we use environment variables (e.g., `.env`) for database URIs and JWT secrets?

Environment variables separate application code from sensitive credentials and environment-specific configuration. Hardcoding database connection strings or JWT secret keys risks exposing them in public source repositories. Storing them in a `.env` file (and listing it in `.gitignore`) keeps production secrets out of version control and safe across team and deployment environments.
