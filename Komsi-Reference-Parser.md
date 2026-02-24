# Specification Reference Parser for the KOMSI-Protocol

Here are some simple example parsers for the KOMSI-Protocol as reference. You are free to use and extend them for whatever purposes you like. But please try to understand them before you use them.

## 1. Rust 

```rust
fn parse_komsi(input: &str) {
    // Process each line separated by \n
    for line in input.lines() {
        let mut chars = line.chars().peekable();
        
        while let Some(c) = chars.next() {
            if c.is_ascii_alphabetic() {
                let cmd = c;
                let mut val_str = String::new();
                
                // Collect all subsequent digits for this command
                while let Some(&next_c) = chars.peek() {
                    if next_c.is_ascii_digit() {
                        val_str.push(chars.next().unwrap());
                    } else {
                        break;
                    }
                }
                
                if !val_str.is_empty() {
                    let val: u32 = val_str.parse().unwrap_or(0);
                    println!("Command: {}, Value: {}", cmd, val);
                }
            }
        }
    }
}
```

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

