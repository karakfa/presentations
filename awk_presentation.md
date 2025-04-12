
---

## marp: true paginate: true theme: default

# Introduction to AWK

- **What is AWK?**
  - AWK is a powerful text-processing language.
  - Named after its creators: **A**ho, **W**einberger, and **K**ernighan.
  - Often used for data extraction and reporting.
- **Why use AWK?**
  - Lightweight
  - Built into Unix/Linux
  - Efficient for processing structured text

---

# Basic Syntax

```bash
awk 'pattern { action }' filename
```

- `pattern` - the condition to match
- `action` - what to do if pattern matches
- `filename` - input file

**Example:**

```bash
awk '{ print $1 }' data.txt
```

Prints the first field of every line.

---

# Structure of an AWK Program

```awk
BEGIN { # Initialization }

pattern1 { action1 }
pattern2 { action2 }

END { # Final steps }
```

- `BEGIN` block: runs before input is processed
- `END` block: runs after all input is processed
- `pattern { action }` blocks are executed on matching lines

---

# AWK Variables

- **Built-in Variables:**
  - `$0` - entire line
  - `$1`, `$2`, ..., `$n` - fields
  - `NR` - number of records (lines) processed
  - `NF` - number of fields in the current record
  - `FS` - field separator
  - `OFS` - output field separator

**Example:**

```bash
awk '{ print "Fields:", NF, "Last Field:", $NF }' file.txt
```

---

# Pattern Matching

- **Regex Matching:**

  ```bash
  awk '/pattern/' file
  ```

- **Comparison Operators:**

  - `==`, `!=`, `<`, `>`, `<=`, `>=`

**Example:**

```bash
awk '$3 > 50 { print $1, $3 }' scores.txt
```

Prints records where the third field is greater than 50.

---

# String Functions

- `length(string)` – returns length
- `substr(string, start, length)` – substring
- `index(string, search)` – position of search
- `tolower(string)` – convert to lowercase
- `toupper(string)` – convert to uppercase

**Example:**

```bash
awk '{ print toupper($0) }' names.txt
```

---

# Arithmetic & Control Structures

- **Arithmetic:**
  - `+`, `-`, `*`, `/`, `%`
- **Control:**
  ```awk
  if (condition) { ... } else { ... }
  for (i = 1; i <= NF; i++) { ... }
  while (condition) { ... }
  ```

**Example:**

```bash
awk '{ sum += $2 } END { print "Total:", sum }' sales.txt
```

---

# Custom Field Separators

- Default field separator is whitespace.
- Change with `-F` or by setting `FS`.

**Examples:**

```bash
awk -F, '{ print $1, $2 }' file.csv
```

```awk
BEGIN { FS=":" } { print $1, $2 }
```

---

# Real-World Examples

1. **Print usernames from /etc/passwd**

```bash
awk -F: '{ print $1 }' /etc/passwd
```

2. **Calculate average score**

```bash
awk '{ total += $2; count++ } END { print total/count }' scores.txt
```

3. **Find lines with “error”**

```bash
awk '/error/' log.txt
```

---

# Summary & Resources

**Key Takeaways:**

- AWK is great for field-based text processing.
- Combines regex, scripting, and reporting.
- Versatile for sysadmins, analysts, and devs.

**Resources:**

- [GNU AWK Manual](https://www.gnu.org/software/gawk/manual/)
- `man awk`
- [awk tutorials on awk.info](http://awk.info)

---

# Appendix: Handy AWK One-Liners

- **Print first field of every line**

  ```bash
  awk '{ print $1 }' file
  ```

- **Print lines where 2nd field > 100**

  ```bash
  awk '$2 > 100' file
  ```

- **Sum values in 3rd column**

  ```bash
  awk '{ sum += $3 } END { print sum }' file
  ```

- **Print number of lines**

  ```bash
  awk 'END { print NR }' file
  ```

- **Print number of fields per line**

  ```bash
  awk '{ print NF }' file
  ```

- **Replace "foo" with "bar"**

  ```bash
  awk '{ gsub(/foo/, "bar"); print }' file
  ```

- **Print last field of each line**

  ```bash
  awk '{ print $NF }' file
  ```

- **Print lines with more than 5 fields**

  ```bash
  awk 'NF > 5' file
  ```

- **Print line numbers with content**

  ```bash
  awk '{ print NR, $0 }' file
  ```

- **Print unique values from a column**

  ```bash
  awk '!a[$1]++' file
  ```
