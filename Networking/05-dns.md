# DNS — Domain Name System

## DNS Record Types

DNS relies on several record types to store different kinds of information about a domain. An A record maps a domain name to an IPv4 address, while an AAAA record performs the same mapping for IPv6. A CNAME record creates an alias, pointing one domain name to another. An MX record specifies which mail server is responsible for handling email for a domain. A TXT record is commonly used for domain verification and anti-spam mechanisms such as SPF and DKIM.

## How DNS Resolution Works

Resolving a domain name into an IP address follows a chain of lookups that only goes as far as necessary to find an answer. A device first checks whether it already has the answer cached locally from a previous lookup; if so, resolution ends immediately. If not, the query is passed to the ISP's DNS resolver, which maintains its own cache and either returns a cached answer or continues the search further.

If neither the local device nor the ISP's resolver has a cached answer, the query proceeds to a root DNS server, which doesn't hold the final answer itself but knows which top-level domain server to consult next. That top-level domain server, in turn, points to the authoritative server responsible for the specific domain being queried. The authoritative server holds the actual, definitive record and returns the real IP address, which is then cached by the intermediate resolvers for a duration defined by the record's time-to-live value, so that subsequent lookups can be resolved more quickly.

There's an important distinction between a recursive resolver and an authoritative server: a recursive resolver is the intermediary that performs the work of tracking down an answer on behalf of a requesting device, while an authoritative server is the actual source of truth, holding the official records that a domain's owner has configured.
