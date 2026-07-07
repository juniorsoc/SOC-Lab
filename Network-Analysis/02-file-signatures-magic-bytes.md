# File Signatures — Magic Bytes

A file extension is just a name — it carries no guarantee about actual content. An attacker can rename a malicious executable to look like an image or document.

The real type is embedded in the file's first bytes ("magic bytes" / file signature):

| Signature (hex) | File type |
|-------------------|-----------|
| `4D 5A` | Windows executable — huge red flag on a file claiming to be something else |
| `FF D8 FF` | JPEG image |
| `89 50 4E 47` | PNG image |
| `25 50 44 46` | PDF |
| `50 4B 03 04` | ZIP archive |

Tools: `file` (identifies real type from magic bytes), `xxd` (hex dump for manual inspection), CyberChef (broader decoding/analysis online).
