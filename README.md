
## Need / problem
In a game API you should not allow anonymous users to create games or send moves.
Without a check, anyone can call the endpoints directly.

## Solution
`requireAuth` is an Express middleware that blocks requests unless the user is authenticated.

## Usage
```js
import express from "express";
import { requireAuth } from "./src/requireAuth.js";

const app = express();

app.use("/api", requireAuth);

# requireAuth Middleware

## Purpose
This middleware is used to protect routes that require an authenticated user.
It prevents unauthenticated users from accessing protected endpoints.

## Problem it solves
In many web applications, certain routes should only be accessible to logged-in users.
Without middleware, this logic would have to be duplicated in every route handler.

This middleware centralizes authentication checks and ensures consistent access control.

## How it works
The middleware checks if `req.user` exists.
If not, it returns HTTP 401 Unauthorized.
If the user exists, the request continues to the next handler.

## Example usage

```js
const express = require("express");
const { requireAuth } = require("./index");

const app = express();

app.get("/protected", requireAuth, (req, res) => {
  res.json({ message: "You are authenticated" });
});

