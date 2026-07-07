# File Signatures — Magic Bytes

| Hex | Type |
|---|---|
| `4D 5A` | .EXE — most important to catch in SOC work |
| `FF D8 FF` | .JPG |
| `89 50 4E 47` | .PNG |
| `25 50 44 46` | .PDF |
| `50 4B 03 04` | .ZIP |

**Why it matters:** a renamed `.exe` disguised as `photo.jpg` is caught by checking the actual hex signature, not the extension.

**Tools:** `file` (identifies real type), `xxd` (hex dump), CyberChef (online decoder).
