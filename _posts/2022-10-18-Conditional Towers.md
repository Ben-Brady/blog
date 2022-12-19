---
layout: post
title:  "Pattern - Conditional Towers"
date:   2022-10-18 +0000
---

A common pattern in code is the use of a conditional tower to isolate an selection process into it's own function.

```python
def get_tax_rate(income: int) -> int:
    if income < 12_570:
        return 0
    elif income < 50_270:
        return 20
    elif income < 150_000:
        return 40
    else:
        return 50
```

A conditional tower allows you extract a selection process into a single function so that it can be seperated from the rest of your code.

However, doing this with a switch statement is ill-advised at the same result could easily be accomplished with a table lookup:

```typescript
function switch_version(code: string) {
    switch (code){
        case "A":
            return 10;
        case "B":
            return 20;
        case "C":
            return 30;
        case "D":
            return 40;
        default:
            return 0;
    }
}
```

However, the same behaviour can be achieved with less code using a table lookup, although this can make shorter functions harder to read, with larger lookups it

```typescript
function lookup_version(code: string) {
    const LOOKUP = {
        "A": 10,
        "B": 20,
        "C": 30,
        "D": 40,
        "E": 55,
        "F": 45,
        "G": 64,
        "H": 74,
        "I": 45,
    }
    return LOOKUP[code] ?? 0;
}
```
