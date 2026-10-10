# Reference example: Express server walkthrough

Use this user-approved example to calibrate top-to-bottom order, short explanations, and concrete inputs and outcomes. It illustrates teaching style; inspect the actual target code rather than assuming it matches this example.

---

This `server.js` creates a web server that responds with **“Hello, world!”** and limits each IP address to **100 requests per one-minute window**.

```js
import express from 'express';
```

First, we import Express, which helps us build a server that receives requests and sends responses.

```js
import dotenv from 'dotenv';
```

We import `dotenv` so the program can load settings from a `.env` file.

```js
import rateLimit from 'express-rate-limit';
```

We import `rateLimit`, which creates a check that blocks excessive requests.

```js
dotenv.config();
```

This loads settings into `process.env`. For example, if `.env` contains `PORT=4000`, the program can read that value through `process.env.PORT`.

```js
const app = express();
```

Calling `express()` creates an application and returns it as `app`. We’ll use `app` to register request handling and start the server.

```js
const PORT = process.env.PORT || 3000;
```

This chooses the port where the server will listen. If `process.env.PORT` is `"4000"`, it uses that; otherwise, `||` supplies the fallback `3000`.

```js
const limiter = rateLimit({
```

We create the request-checking function and store it as `limiter`. The settings inside `{ ... }` determine when it blocks requests.

```js
    windowMs: 1 * 60 * 1000, // 1 minute
```

This sets the counting window in milliseconds: **1 minute × 60 seconds × 1,000 milliseconds = 60,000 milliseconds**.

```js
    limit: 100, // limit each IP to 100 requests per minute
});
```

This allows 100 requests from each IP within that window. If the same IP sends a 101st request before its window resets, the limiter responds with **429 — Too Many Requests**.

```js
app.use(limiter);
```

We attach the check before the route below. A function that checks requests along the way is called **middleware**: allowed requests continue; blocked requests receive the limiter’s response.

```js
app.get('/', (req, res) => {
```

We register a function to handle GET requests to `/`, the server’s root address. `req` represents the incoming request, and `res` lets us respond; this function runs when a matching request arrives.

```js
  res.send('Hello, world!');
});
```

This sends `Hello, world!` back to the requester. For example, an allowed GET request to `http://localhost:3000/` receives that text.

```js
app.listen(PORT, () => {
```

This starts the server listening on the chosen port. The function written as `() => { ... }` runs once the server starts listening.

```js
  console.log(`Server is running on port ${PORT}`);
});
```

This prints the startup message in the terminal. With `PORT` set to `3000`, `${PORT}` inserts that value, producing `Server is running on port 3000`.

For example, with a fresh limit window, opening `http://localhost:3000/` sends a request through the limiter to the route, which replies **“Hello, world!”** After 100 requests from that IP within the window, further requests receive **429** until the window resets. This is expected behavior from the source; I haven’t started the server.
