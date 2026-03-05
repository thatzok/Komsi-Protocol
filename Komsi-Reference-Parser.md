# Specification Reference Parser for the KOMSI-Protocol

Here are some simple example parsers for the KOMSI-Protocol as reference. You are free to use and extend them for whatever purposes you like. But please try to understand them before you use them.

## 1. Rust 

If you are using Rust, it is recommended to use the type-safe

[<img alt="github" src="https://img.shields.io/badge/github-thatzok/komsi--lib-8da0cb?style=for-the-badge&labelColor=555555&logo=github" height="20">](https://github.com/thatzok/komsi-lib)
[<img alt="crates.io" src="https://img.shields.io/crates/v/komsi.svg?style=for-the-badge&color=fc8d62&logo=rust" height="20">](https://crates.io/crates/komsi)


## 2. C

```C
#include <stdio.h>
#include <ctype.h>
#include <stdlib.h>

void parse_komsi(const char* data) {
    const char* ptr = data;
    while (*ptr) {
        if (isalpha(*ptr)) {
            char cmd = *ptr++;
            char* end_ptr;
            // strtoul automatically stops at the first non-digit character
            unsigned long val = strtoul(ptr, &end_ptr, 10);
            
            if (ptr != end_ptr) {
                printf("Command: %c, Value: %lu\n", cmd, val);
                ptr = end_ptr; // Move pointer to the end of the number
            }
        } else {
            ptr++; // Skip unknown characters or LF
        }
    }
}
```

## 3. PHP

```PHP
function parseKomsi($input) {
    // Split input into lines by LF
    $lines = explode("\n", $input);
    
    foreach ($lines as $line) {
        // Regex: 1 Letter ([a-zA-Z]) followed by 1+ Digits (\d+)
        preg_match_all('/([a-zA-Z])(\d+)/', $line, $matches, PREG_SET_ORDER);
        
        foreach ($matches as $match) {
            $cmd = $match[1];
            $val = (int)$match[2];
            echo "Command: $cmd, Value: $val\n";
        }
    }
}
```

## 4. Python

```python
import re

def parse_komsi(data: str):
    # Pattern: Captures one letter and the following integer sequence
    pattern = re.compile(r'([a-zA-Z])(\d+)')
    
    # Iterate through all matches found in the input string
    for match in pattern.finditer(data):
        cmd, val = match.groups()
        print(f"Command: {cmd}, Value: {int(val)}")

# Usage Example
data = "A100b50\nC999"
parse_komsi(data)
```

Have fun!

