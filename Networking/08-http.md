# HTTP

HTTP is **stateless** — the server has no memory between requests. **Sessions + cookies** solve this: login creates a session ID stored in a cookie, sent automatically on every request. **Session hijacking** = stealing that cookie to impersonate a user (look for one session ID from two IPs at once).

**URL structure:** `scheme://user:pass@host:port/path?query#fragment`

**HTTP methods:** GET (retrieve), POST (submit), PUT (update), DELETE (remove). Bursts of DELETE/POST/PUT from one IP can indicate abuse or brute-forcing.

**Status codes:** 2xx success, 3xx redirect, 4xx client error, 5xx server error. Key ones: 200 OK, 401 Unauthorized, 403 Forbidden, 404 Not Found, 500 Server Error. A spike in 404s = directory scanning; spike in 401/403 = break-in attempt.

**Headers to watch:** `User-Agent: python-requests`/`curl` instead of a browser = suspicious. Missing `Host` header, unusual `Cookie` values, or mismatched `Content-Type` are all red flags.
