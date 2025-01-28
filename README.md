# Dirsearch_Help
Here’s a complete guide to **Dirsearch** help options with examples:

---

## **Basic Usage**
Run a simple directory scan:
```bash
dirsearch -u http://example.com/
```

### **Full Help Command**
To see all options:
```bash
dirsearch --help
```

---

## **1. Target Options**
| Option | Description | Example |
|--------|-------------|---------|
| `-u`, `--url` | Target URL | `dirsearch -u http://example.com/` |
| `-l`, `--url-list` | Scan multiple URLs from a file | `dirsearch -l urls.txt` |
| `--exclude-urls` | Exclude specific URLs | `dirsearch -u http://example.com/ --exclude-urls logout,admin` |
| `--subdirs` | Scan specific subdirectories | `dirsearch -u http://example.com/ --subdirs /admin,/images` |

---

## **2. Request Options**
| Option | Description | Example |
|--------|-------------|---------|
| `-m`, `--method` | HTTP method (GET, POST, etc.) | `dirsearch -u http://example.com/ -m POST` |
| `--header` | Add custom headers | `dirsearch -u http://example.com/ --header "User-Agent: custom"` |
| `--cookie` | Use a session cookie | `dirsearch -u http://example.com/ --cookie "PHPSESSID=12345"` |
| `--auth` | HTTP Basic Authentication | `dirsearch -u http://example.com/ --auth admin:password` |
| `--user-agent` | Set custom User-Agent | `dirsearch -u http://example.com/ --user-agent "Mozilla/5.0"` |
| `--proxy` | Use a proxy | `dirsearch -u http://example.com/ --proxy http://127.0.0.1:8080` |

---

## **3. Performance Options**
| Option | Description | Example |
|--------|-------------|---------|
| `-t`, `--threads` | Set number of threads | `dirsearch -u http://example.com/ -t 50` |
| `--delay` | Delay between requests | `dirsearch -u http://example.com/ --delay 1` |
| `--timeout` | Set timeout in seconds | `dirsearch -u http://example.com/ --timeout 10` |
| `--max-rate` | Limit requests per second | `dirsearch -u http://example.com/ --max-rate 5` |

---

## **4. Dictionary Options**
| Option | Description | Example |
|--------|-------------|---------|
| `-w`, `--wordlist` | Use a custom wordlist | `dirsearch -u http://example.com/ -w custom.txt` |
| `--extensions` | File extensions to search | `dirsearch -u http://example.com/ --extensions php,html,js` |
| `--exclude-extensions` | Exclude file types | `dirsearch -u http://example.com/ --exclude-extensions jpg,png` |

---

## **5. Filtering & Reporting**
| Option | Description | Example |
|--------|-------------|---------|
| `--exclude-status` | Ignore specific status codes | `dirsearch -u http://example.com/ --exclude-status 404,403` |
| `--min-response-size` | Minimum response size | `dirsearch -u http://example.com/ --min-response-size 1000` |
| `--max-response-size` | Maximum response size | `dirsearch -u http://example.com/ --max-response-size 5000` |
| `--format` | Output format (json, csv, xml) | `dirsearch -u http://example.com/ --format json` |
| `--output` | Save output to a file | `dirsearch -u http://example.com/ --output results.txt` |

---

## **6. Miscellaneous Options**
| Option | Description | Example |
|--------|-------------|---------|
| `--deep-recursive` | Recursive search with full paths | `dirsearch -u http://example.com/ --deep-recursive` |
| `--random-agent` | Use a random User-Agent | `dirsearch -u http://example.com/ --random-agent` |
| `--quiet-mode` | Suppress output (useful for scripts) | `dirsearch -u http://example.com/ --quiet-mode` |

---

## **Example Commands**
1️⃣ **Basic Scan with Default Settings**
```bash
dirsearch -u http://example.com/
```

2️⃣ **Scan Multiple URLs from a File**
```bash
dirsearch -l targets.txt
```

3️⃣ **Use a Custom Wordlist**
```bash
dirsearch -u http://example.com/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

4️⃣ **Scan with Specific File Extensions**
```bash
dirsearch -u http://example.com/ --extensions php,html,js
```

5️⃣ **Scan Using a Proxy (e.g., Burp Suite)**
```bash
dirsearch -u http://example.com/ --proxy http://127.0.0.1:8080
```

6️⃣ **Save Results in JSON Format**
```bash
dirsearch -u http://example.com/ --format json --output results.json
```

Let me know if you need more details! 🚀
