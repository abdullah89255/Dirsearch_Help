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



# Quick reference (most-used flags)

* `-u` target URL (or `-L targets.txt`)
* `-w` wordlist file (one entry per line)
* `-e` extensions (comma-separated: `php,html,js,txt`)
* `-t` threads (concurrency)
* `--recursive` try directories recursively (one level)
* `--deep-recursive` deeper recursion (be careful—explodes requests)
* `--force-extensions` append extensions even if the word contains a dot
* `-x` exclude HTTP status codes (e.g. `-x 400,404`)
* `--timeout` request timeout seconds
* `--delay` delay between requests (seconds)
* `--random-agent` randomize User-Agent
* `--proxy` `http://127.0.0.1:8080` (for Burp/mitm)
* `-H` custom HTTP header (e.g. `-H "Host: secret.example.com"`)
* `--plain-text-report=out.txt` save results

---

# Basic fuzz example

Brute-force common dirs + extensions:

```bash
dirsearch -u https://target.com -w /usr/share/wordlists/dirb/common.txt -e php,html,js,txt -t 40 --random-agent --plain-text-report=dirsearch.txt
```

---

# Deep recursion (discover nested dirs)

Be careful — this multiplies requests:

```bash
dirsearch -u https://target.com -w biglist.txt -e php,html,js --recursive --deep-recursive -t 30 --timeout=10
```

---

# Skip noisy status codes (reduce false positives)

Exclude 404 and 400 responses so you only see interesting ones:

```bash
dirsearch -u https://target.com -w list.txt -e php,html -x 400,404 --plain-text-report=out.txt
```

---

# Force extension behavior (useful for APIs/static)

If words look like `api/v1/users` and you still want `.json`, use:

```bash
dirsearch -u https://target.com -w endpoints.txt -e json --force-extensions
```

---

# Virtual host / vHost fuzzing

Some sites host multiple apps by Host header. Use `-H` to fuzz vhosts or add Host header list:

```bash
dirsearch -u https://target.com -w vhosts.txt -e "" -H "Host: FUZZ.target.com"
```

(If dirsearch doesn’t do `'FUZZ'` header substitution, generate headers list and run multiple runs with script/for-loop.)

---

# Use custom headers (auth/CSRF simulation)

```bash
dirsearch -u https://target.com -w list.txt -H "Authorization: Bearer ABC" -H "X-CSRF-Token: token" --random-agent
```

---

# Slow and stealthy (bypass WAF / avoid rate-limiting)

```bash
dirsearch -u https://target.com -w stealth.txt -t 5 --delay 0.5 --timeout 10 --random-agent
```

---

# Combine with JS/Wayback-derived words (best practice)

1. Extract candidate paths from JS/Wayback/GitHub (tools: `gau`, `waybackurls`, `wayback_machine_downloader`)
2. Deduplicate and use as wordlist:

```bash
cat js_paths.txt wayback_paths.txt | sort -u > combined.txt
dirsearch -u https://target.com -w combined.txt -e php,html,js,txt --plain-text-report=combined_report.txt
```

---

# Wordlists — what to use

* small: `common.txt` (fast discovery)
* medium: `raft-small-directories.txt`, `dirbuster medium`
* large: `seclists/Discovery/Web-Content/` (huge, use with care)
* custom: generate from JS, Wayback, sitemap.xml, or `cewl` to create targeted lists

---

# When dirsearch is NOT the right tool

* **Parameter fuzzing**, POST/JSON endpoints, or injection tests → use `ffuf`, `wfuzz`, or `Burp Intruder`.
  Example: fuzzing GET param `id` with ffuf:

  ```bash
  ffuf -u https://target.com/page.php?id=FUZZ -w ids.txt
  ```
* **API JSON** fuzzing (body payloads) → `ffuf` supports `-d` and `-H "Content-Type: application/json"`.

---

# Parsing & triaging results

* Save plain report: `--plain-text-report=out.txt`
* Filter for interesting codes:

```bash
grep -E "200|301|302|403" dirsearch.txt | sort -u
```

* Check content lengths to spot unusual pages:

```bash
awk -F ' ' '$3 ~ /200|301|302|403/ {print $0}' dirsearch.txt | sort -k4 -n
```

(Format depends on your report; tweak as needed.)

---

# Practical sessions/recipes

1. Fast reconnaissance (discovery, low noise):

```bash
dirsearch -u https://target.com -w /usr/share/wordlists/dirb/common.txt -e php,html,js --random-agent -t 25 --timeout 7 --plain-text-report=fast.txt
```

2. Focused JS + API hunt (use extracted words + extensions):

```bash
cat js_words.txt wayback_words.txt | sort -u > api_candidates.txt
dirsearch -u https://target.com -w api_candidates.txt -e php,html,js,json --force-extensions -t 20 --plain-text-report=api_report.txt
```

3. Stealth deep scan (slow to evade defense):

```bash
dirsearch -u https://target.com -w biglist.txt -e php,html --recursive -t 4 --delay 1 --timeout 15 --random-agent --plain-text-report=stealth.txt
```

---

# Extra tips & common pitfalls

* **Start small**, then expand lists. Large lists with deep recursion will take forever and generate noise.
* **Use proxies** (Burp) to inspect interesting responses and confirm actual content — 200 on 404 pages (WAF/content gating) is common.
* **Look at content-length / reflection** — two 200 responses with different content-lengths likely mean real pages.
* **403s can be interesting** — sometimes indicate an existing resource requiring auth (bruteforce login paths).
* **Sitemaps** (`/sitemap.xml`) and `robots.txt` are low-hanging fruit; always fetch them first.
* **Combine tools**: dirsearch for directories/files, ffuf/wfuzz for parameter fuzzing, Burp for manual validation.

---

If you want, I can:

* Give a one-line alias for `~/.bashrc` that hides the DeprecationWarning and runs dirsearch (from earlier).
* Build a ready `combined.txt` workflow using `gau`/`waybackurls` (I can show commands you can paste).
* Show an example `ffuf` command for parameter fuzzing.

Which of those do you want next?

