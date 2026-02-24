# KOMSI Command Structure (KCS) Specification

## 1. Protocol Overview

The KOMSI protocol is a **unidirectional, ASCII-based, line-oriented** communication protocol. It is designed for
high-speed parsing with minimal overhead by using a strict `<code><value>` format without internal delimiters.

* **Encoding:** Standard ASCII.
* **Termination:** Every message line must end with a Line Feed (`LF`, ASCII 10).
* **Tolerance:** Carriage Return (`CR`, ASCII 13) characters are permitted at the beginning or end of a line (before or
  after an `LF`) but must be **ignored** by the parser.
* **Case Sensitivity:** Command codes are **case-sensitive** (e.g., `a` is different from `A`).

## 2. Formal Grammar (ABNF)

The following [Augmented Backus-Naur Form (RFC 5234)](https://datatracker.ietf.org) defines the syntax.

```abnf
; Protocol Rules
komsi-protocol = *line
line           = *CR 1*variable *CR LF *CR

; A variable is a command-code immediately followed by a digit sequence
variable       = command-code value

; Command-code is exactly one case-sensitive letter
command-code   = %x41-5A / %x61-7A  ; A-Z / a-z

; Value is one or more digits
value          = 1*DIGIT

; Terminals
DIGIT          = %x30-39            ; 0-9
LF             = %x0A               ; Line Feed (\n)
CR             = %x0D               ; Carriage Return (\r) - Ignored
```

## 3. Structural Constraints

To ensure reliable implementation, the following rules apply:

| Feature                     | Requirement                                                                                                                                                                                                                                                                                                                                                        |
|:----------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Separators**              | No whitespace is allowed between `command-code` and `value`, nor between multiple `variables` in a single line.                                                                                                                                                                                                                                                    |
| **Line Ending**             | `LF` is the mandatory terminator. `CR` is ignored if present.                                                                                                                                                                                                                                                                                                      |
| **Value Handling**          | Most values are treated as integers. Command `r` (DateTime) must be handled as a **fixed-width numeric string**.                                                                                                                                                                                                                                                   |
| **Empty Lines**             | Empty lines (just `LF` or `CRLF`) are permitted but contain no commands and are ignored.                                                                                                                                                                                                                                                                           |
| **Ordering**                | The sequence of variables within a line is preserved and may be semantically significant.                                                                                                                                                                                                                                                                          |
| **Partial or Full Updates** | For efficiency and small data footprint it is expected that only changed values are transmitted. However, the sending application decides how often and how many values are transmited. If a sending application sends all values in one line the receiving application MUST be able to process this and **MUST MAKE SURE** there is **no input buffer-overflow**. |

## 4. Examples

| Input String        | Description                                 |
|:--------------------|:--------------------------------------------|
| `A1\n`              | Ignition ON                                 |
| `y50t2500\n`        | Speed 50 km/h and RPM 2500 in one line.     |
| `o1500450\n`        | Odometer at 1,500,450 meters (1,500.45 km). |
| `r20241224180000\n` | Date set to Dec 24, 2024, at 18:00:00.      | 


