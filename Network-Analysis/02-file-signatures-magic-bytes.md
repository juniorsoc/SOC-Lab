# File Signatures — Magic Bytes

A file's extension is simply a naming convention and carries no inherent guarantee about what the file actually contains — an attacker can freely rename a malicious executable to appear as an ordinary image or document. The file's true type, however, is embedded in its actual content, in the form of a short sequence of bytes at the very beginning of the file known as its magic bytes or file signature, which identifies the format regardless of whatever extension has been applied to it.

Certain signatures recur often enough to be worth recognizing on sight. A signature beginning with `4D 5A` identifies a Windows executable, and encountering this signature on a file claiming to be something else — an image, a document — is one of the most significant red flags a SOC analyst can encounter, since it indicates a deliberate attempt to disguise executable code. Signatures such as `FF D8 FF` and `89 50 4E 47` correspond to standard image formats, and files bearing these signatures alongside unexpected extensions warrant closer inspection to rule out a payload hidden within what otherwise appears to be an ordinary image. Similarly, `25 50 44 46` identifies a PDF document, and `50 4B 03 04` identifies a ZIP archive, both of which are common vectors for delivering malicious content disguised as an innocuous attachment.

Several tools support this kind of inspection directly. On Linux, a dedicated command identifies a file's actual type by examining its magic bytes rather than trusting its extension, while another displays a file's raw contents as a hexadecimal dump for manual inspection. Online tools such as CyberChef provide a broader set of decoding and analysis capabilities for examining suspicious content in more depth.

## Practical Example — Verifying a Suspicious Attachment

```bash
$ file invoice.pdf
invoice.pdf: PE32+ executable (GUI) x86-64, for MS Windows

$ xxd invoice.pdf | head -2
00000000: 4d5a 9000 0300 0000 0400 0000 ffff 0000  MZ..............
00000010: b800 0000 0000 0000 4000 0000 0000 0000  @...............
```

Despite the `.pdf` extension and filename suggesting an invoice, the `file` command immediately identifies it as a Windows executable, and the hex dump confirms it starting with `4D 5A` (`MZ` in ASCII) — the exact executable signature covered above. This is a textbook example of a malicious file disguised as a harmless document, exactly the kind of check worth running on any suspicious email attachment before it's opened.
