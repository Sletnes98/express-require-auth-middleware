# requireAuth Middleware

## Need / problem
In a game API you should not allow anonymous users to create games or send moves.
Without an authentication check, anyone can call protected endpoints directly.

## Solution
`requireAuth` is an Express middleware that blocks requests unless the user is authenticated.

## Purpose
This middleware is used to protect routes that require an authenticated user.
It prevents unauthenticated users from accessing protected endpoints.

## Problem it solves
In many web applications, certain routes should only be accessible to logged-in users.
Without middleware, this logic would have to be duplicated in every route handler.

This middleware centralizes authentication checks and ensures consistent access control.

## How it works
The middleware checks if `req.user` exists.

- If `req.user` does not exist, it returns HTTP 401 Unauthorized.
- If `req.user` exists, the request continues to the next handler.

The middleware assumes authentication has already happened earlier in the request flow
(for example via session or token-based authentication).

## Example usage

```js
import express from "express";
import { requireAuth } from "./src/requireAuth.js";

const app = express();

app.use("/api", requireAuth);

app.get("/api/protected", (req, res) => {
  res.json({ message: "You are authenticated" });
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
