# Distributed URL Shortener

A scalable URL shortening service built with a focus on backend system 
design — caching, efficient encoding, and horizontal scalability — 
rather than just CRUD functionality.

## Features
- Base62 encoding for compact, unique short codes
- Custom-built LRU cache layer to reduce database load on frequent lookups
- SQL-backed persistent storage for URL mappings
- Architecture designed for horizontal scaling via sharding

## Architecture
- **ID Generation:** Auto-incrementing ID converted to a Base62 string, 
  producing short, URL-safe codes (e.g., `id=125 → "cb"`)
- **Storage:** SQL database stores the mapping between short codes and 
  original URLs, with indexing on the short code for fast lookups
- **Caching:** A custom-built LRU cache sits in front of the database, 
  serving frequently accessed URLs without hitting SQL on every request
- **Scalability:** Sharding strategy (by hash range of short code) 
  designed to distribute load across multiple DB instances as traffic grows

## Tech Stack
C++, SQL, Caching (LRU), System Design

## How to Run
\`\`\`bash
g++ -std=c++17 main.cpp -o urlshortener
./urlshortener
\`\`\`

## Example Usage
\`\`\`
> shorten("https://example.com/very/long/url")
Short URL: short.ly/cb
> resolve("short.ly/cb")
https://example.com/very/long/url
\`\`\`

## What I Learned
This project helped me understand the trade-offs between [cache 
consistency, encoding collision handling, and scaling reads vs writes 
— fill in what's actually true once you've built and hit real design 
decisions].
