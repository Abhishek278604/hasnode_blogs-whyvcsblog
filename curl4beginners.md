# cURL for Beginners: Your First Steps to Talking to Servers

# Background:

Ever wondered how apps fetch data from the internet or how developers test their APIs directly, without using a web browser. Here in this article we are going to see how **cURL** command method fulfills this need. cURL is a simple, yet powerful tool that every programmer must know about.

In this article, we will learn about basics of any cURL request, and some other small but important cURL command flag options like `-i` and `-k` etc.

---

## What is a Server:

Before we dive into cURL, let's understand what we're talking *to*.

Think of a **server** as a computer or a cloud compute instance which is always online, waiting to answer questions. When you open a website, your browser sends a request to a server, and the server sends back the webpage of the website you were trying to open.

```
You (Browser) → "Hey, give me google.com" → Server
Server → "Here's the webpage for google.com" → You (Browser)
```

This back and forth conversation happens millions of times every second across the internet. Your browser does this automatically. But what if you want to do it manually because you are a developer and you want to test some API endpoints or open a website, this is exactly where cURL comes into picture.

---

## What is cURL:

**cURL** (pronounced "curl") stands for "Client URL." In simple terms:

> cURL is a command-line tool that lets you send requests to servers and see what they send back.

Instead of using a browser with buttons and visuals, you type a command in your terminal, and cURL does the talking for you.

Think of it like this:

| Browser | cURL |
|---------|------|
| Visual interface | Text-based commands |
| Click links, fill forms | Type commands |
| Hides the technical details | Shows you everything |

Both do the same thing — talk to servers. But cURL gives you full control and visibility.

---

## Why Do Programmers Need cURL:

You might ask, "Why can't we just use a browser only"

Below are the reasons why cURL is essential for developers:

1. **Testing APIs** — When building apps, you need to test if your server responds correctly. cURL lets you do this instantly.

2. **Automation** — You can write scripts that make hundreds of requests automatically.

3. **Debugging** — See exactly what's being sent and received, including hidden headers.

4. **No GUI needed** — Works on servers that don't have a screen or browser installed.

5. **Speed** — Much faster than opening a browser for quick checks.


---

## Where cURL Fits in Development Cycle or Developer's Workflow:

Below is a simple diagram showing when developers typically use cURL:

```
┌─────────────────────────────────────────────────────────┐
│                  Developer's Workflow                   │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   Write Code → Test with cURL → Debug → Deploy          │
│                      ↓                                  │
│              ┌──────────────┐                           │
│              │    Server    │                           │
│              │   (Your API) │                           │
│              └──────────────┘                           │
│                      ↑                                  │
│   cURL: "Does this endpoint work?"                      │
│   Server: "Yes, here's the data!"                       │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Make Your First Request with cURL: 

Open your terminal and type:

```bash
curl https://example.com
```

and hit 'Enter'. You should see a bunch of HTML code appear in your terminal. Here whatever you see in the output of the previous curl command actually represent the webpage for the website example.com !


### What actually happened in the above curl command you ran or request you made:

```
┌──────────┐         Request          ┌──────────┐
│          │  ──────────────────────► │          │
│   You    │   "GET example.com"      │  Server  │
│ (cURL)   │                          │          │
│          │  ◄────────────────────── │          │
└──────────┘        Response          └──────────┘
                  (HTML content)
```

1. cURL sent a **request** to example.com
2. The server received it and sent back a **response**
3. cURL displayed that response in your terminal in the form of HTML sort of code.

---

## Understanding Request and Response

Every time you use cURL (or a browser), there's a conversation happening behind the scene:

### The Request (Represents what you asked for or what you sent):

A request contains:
- **URL** — Where you want to go (e.g., `https://chai-code.com`)
- **Method or Type of Request** — What you want to do (GET, POST, etc.)
- **Headers** — Extra information (like your browser type)
- **Body or Data You Sent With Request** — Data you're sending (for POST requests)

### The Response (Represent the result you got in return):

A response contains:
- **Status Code** — Did it work? (200 = success, 404 = not found)
- **Headers** — Information about the response
- **Body** — The actual content (HTML, JSON, etc.)

To see more details in your response add the `-i` flag option in the curl request:

```bash
curl -i https://chai-code.com
```

Now you will see the response headers too:

```
HTTP/1.1 200 OK
Content-Type: text/html
...

<!DOCTYPE html>
<html>
...
```

That `200 OK` you see above in response means the request was successful and it is called the Status Code of the request!

### These are some of the very common status codes we encounter frequently:

| Code | Meaning |
|------|---------|
| 200 | Success — everything worked |
| 201 | Created — new resource was made |
| 400 | Bad Request — something's wrong with your request |
| 404 | Not Found — the page doesn't exist |
| 500 | Server Error — something broke on their end |

---

## Browser vs cURL:

Here is what happens behind the scenes:

```
In Case of Browser Request:
┌─────────────────────────────────────────────────────────┐
│                    BROWSER REQUEST                      │
├─────────────────────────────────────────────────────────┤
│  1. You type URL                                        │
│  2. Browser sends request (hidden)                      │
│  3. Browser receives HTML (hidden)                      │
│  4. Browser renders pretty webpage ← You see this       │
└─────────────────────────────────────────────────────────┘

In Case of cURL Request:
┌─────────────────────────────────────────────────────────┐
│                     cURL REQUEST                        │
├─────────────────────────────────────────────────────────┤
│  1. You type: curl https://example.com                  │
│  2. cURL sends request ← You control this               │
│  3. cURL shows raw response ← You see everything        │
│  4. No rendering, just data                             │
└─────────────────────────────────────────────────────────┘
```

Same conversations, different done with different methods and with different visual output/response structures. The cURL shows you the raw code behind the scene of the wepage searched. But Browser Request returns better visual output of the webpage searched for rather than raw code.

---

## Using cURL to Talk to APIs

APIs (Application Programming Interfaces) are how apps talk to each other. Let's try a real one.

### Making a GET Request

GET requests *fetch* data. It's like asking a question.

```bash
curl https://jsonplaceholder.typicode.com/posts/1
```

You'll get back JSON data:

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati",
  "body": "quia et suscipit..."
}
```

This is how apps fetch user profiles, product listings, news articles, and more.

### Making a POST Request

POST requests *send* data. It's like submitting a form.

```bash
curl -X POST https://jsonplaceholder.typicode.com/posts \
  -H "Content-Type: application/json" \
  -d '{"title": "My Post", "body": "Hello World!", "userId": 1}'
```

Let's break this down:
- `-X POST` — We're sending data, not just fetching
- `-H "Content-Type: application/json"` — We're sending JSON format
- `-d '...'` — The actual data we're sending

The server responds with your created post:

```json
{
  "title": "My Post",
  "body": "Hello World!",
  "userId": 1,
  "id": 101
}
```

### GET vs POST: Quick Summary

```
┌────────────────────────────────────────────────┐
│                GET Request                     │
│  "Give me information"                         │
│  Example: Viewing a profile                    │
│  curl https://api.com/users/123                │
├────────────────────────────────────────────────┤
│                POST Request                    │
│  "Here's some information to save"             │
│  Example: Creating a new account               │
│  curl -X POST https://api.com/users -d '...'   │
└────────────────────────────────────────────────┘
```

---

## Common Mistakes Which Beginners Make:

Learning from others' mistakes can save you hours of frustration:

### 1. Forgetting the Protocol

```bash
# Wrong
curl example.com

# Right
curl https://example.com
```

Always include `http://` or `https://`.

### 2. Wrong Quotes on Windows

Windows and UNIX-like(Linux/Mac) Command Prompt use different quote pattern:

```bash
# Linux/Mac
curl -d '{"name": "John"}'

# Windows CMD
curl -d "{\"name\": \"John\"}"
```

So based on above, please use the relevant quotes format supported by your Operating System while contructing a cURL request.

### 3. Missing Content-Type Header

When you are sending data in JSON format in side the body of cURL request, always specify the 'Content-Type'it:

```bash
# Missing header — might not work
curl -X POST https://api.com/data -d '{"key": "value"}'

# With header — reliable
curl -X POST https://api.com/data \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'
```

### 4. Not Checking the Response Code

If you want to avoid your request to fail silently. Use `-i` flag option with the cURL request to see the status code clearly:

```bash
curl -i https://api.com/endpoint
```

If you see `400` or `500` errors, something is wrong.

### 5. Copying Commands with Smart Quotes

Blog posts sometimes use curly quotes (" ") instead of straight quotes (" "). Your terminal won't understand them. Always retype quotes if a command does not work.

### 6. Ignoring SSL Errors

Sometimes you will see certain SSL certificate errors. Use `-k` flag option with your cURL request command to bypass these SSL erros. Remember us `-k` flag only your local development enviroment:

```bash
# Only for testing locally!
curl -k https://localhost:8080/api
```

**Never use `-k` with real websites.**

---

## Quick Reference: Essential cURL Commands

Here are the commands we covered, all in one place:

```bash
# Basic GET request
curl https://example.com

# See response headers
curl -i https://example.com

# POST request with JSON
curl -X POST https://api.com/endpoint \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'

# Save response to file
curl https://example.com -o page.html

# Follow redirects
curl -L https://short-url.com
```

---

## Try It Yourself:

The best way to learn is to practice. Pick an API (like the free [JSONPlaceholder](https://www.chaicode.com/) and experiment!

---

## Wrapping Up

cURL might seem intimidating at first, but it's really just a way to have conversations with servers. Instead of sending a request through a browser, you can type exactly what you want to search.

Simply try to `Fetch` a webpage. Then further try to make cURL request to any of the freely available APIs e.g. Google API

---

*If this article seems helpful . Please follow my blog for more beginner friendly programming related articles!*
