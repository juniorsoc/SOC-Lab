# HTTP — Statelessness, Sessions, Structure

## Statelessness and sessions

HTTP (with or without TLS, the "S" in HTTPS) is stateless — every request is independent, server remembers nothing on its own. Problem for anything needing continuity (e.g. staying logged in).

**Solution:** sessions + cookies. On login, server generates a session ID, stores it in a cookie on the client. Every later request auto-includes that cookie.

**Session hijacking:** if an attacker steals a valid session ID from a victim's cookie, they can impersonate that user — no password needed, since the server can't tell the difference.

## URL structure

`scheme://[user@]host[:port]/path?query#fragment`

| Part | Purpose |
|------|---------|
| Scheme | Protocol (HTTP/HTTPS) |
| Host | Server being contacted |
| Port | Which service on that server (defaults per scheme) |
| Path | Specific resource |
| Query | Extra parameters |
| Fragment | Location within the resource, handled client-side |

## Requests / responses

Request = method + path + version + headers. Key request headers: `User-Agent` (what's making the request — automated tools stand out), `Referer` (what linked here).

Response = status line + headers. Key response headers: `Server` (software/version — useful for probing known vulns), `Content-Type` (mismatch with actual content = possible disguise attempt).

## HTTP methods

| Method | Does |
|--------|------|
| GET | Retrieve data, no changes |
| POST | Submit new data (login, create record) |
| PUT | Update existing resource |
| DELETE | Remove resource |

Pattern spotting: a burst of POST at a login endpoint = credential-guessing attempt. Unexpected PUT/DELETE on sensitive resources = possible tampering.

## Status codes

| Range | Means |
|-------|-------|
| 2xx | Success |
| 3xx | Resource moved |
| 4xx | Client-side problem |
| 5xx | Server-side problem |

Common ones: `200` OK, `401` auth required, `403` access denied, `404` not found, `500` server error.

Investigative signal: burst of `404`s from one IP = scanning for hidden files/dirs. Burst of `401`/`403` = unauthorized access attempts.

## Headers

Request: `Host` (which site), `Content-Length`, `Accept-Encoding`, `Cookie` (session ID, etc).
Response: `Set-Cookie`, `Cache-Control`, `Content-Type`, `Content-Encoding`.

Red flags in headers: scripting-library `User-Agent` instead of a browser, missing `Host` where expected, duplicated/unexpected `Cookie` (possible stolen session), mismatched `Content-Type`.
