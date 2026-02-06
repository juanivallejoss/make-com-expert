---
name: make-com-expert
description: >
  Expert-level Make.com (formerly Integromat) automation development skill covering all built-in
  functions, syntax rules, and common patterns. Use this skill whenever the user needs help writing
  Make.com formulas, mapping expressions, scenario logic, data transformations, or debugging
  Make.com function errors. Triggers include: any mention of "Make.com", "Make scenario",
  "Make formula", "Make function", Make.com module fields, mapping panel expressions, or
  questions about formatDate, parseDate, if/switch, get, map, split, replace, or any other
  Make.com built-in function. Also use when the user is building or debugging Make.com
  automation workflows that require data transformation expressions.
---

# Make.com Functions Expert

## Critical: Make.com Is NOT JavaScript

**This is the single most important rule.** Make.com has its own expression language that looks similar to JavaScript but is fundamentally different. Never suggest JavaScript syntax in Make.com formula fields.

### Key Syntax Differences

| Concept | Make.com ✅ | JavaScript ❌ |
|---|---|---|
| Parameter separator | Semicolon `;` | Comma `,` |
| Expression wrapper | `{{expression}}` | None |
| String concatenation | Direct adjacency or `{{a}}{{b}}` | `a + b` |
| Ternary/conditional | `if(expr; val1; val2)` | `expr ? val1 : val2` |
| Equality | `=` | `===` or `==` |
| Not equal | `!=` | `!==` |
| Logical AND | `and` | `&&` |
| Logical OR | `or` | `\|\|` |
| Array index | Starts at **1** | Starts at 0 |
| Null check | `ifempty(val; fallback)` | `val ?? fallback` |
| Object access | `get(obj; path)` or dot notation in mappings | `obj.path` or `obj['path']` |
| Regex in replace | `/pattern/flags` (no named groups) | Full regex support |
| Switch statement | `switch(expr; v1; r1; v2; r2; else)` | `switch(expr) { case... }` |
| String methods | `lower(text)`, `upper(text)` | `text.toLowerCase()` |
| Array iteration | `map(array; key)` function | `.map(x => x.key)` |

### The Semicolon Rule

**All function parameters are separated by semicolons `;`, never commas.**
Commas inside function calls are treated as literal text, not separators.

```
✅ if(1.status = "active"; "yes"; "no")
❌ if(1.status === "active", "yes", "no")

✅ substring(1.name; 0; 3)
❌ 1.name.substring(0, 3)

✅ formatDate(now; "YYYY-MM-DD")
❌ new Date().toISOString()
```

### The Double-Curly-Brace Rule

All expressions in Make.com mapping fields must be wrapped in `{{ }}`. When referencing module output, use the module position number: `1.fieldName`, `2.fieldName`, etc.

```
{{if(1.status = "active"; "Active User"; "Inactive User")}}
{{formatDate(now; "YYYY-MM-DD HH:mm")}}
{{1.firstName}} {{1.lastName}}
```

Text outside `{{ }}` is treated as literal text. You can mix:
```
Hello {{1.name}}, your order #{{2.orderId}} is {{if(2.shipped; "shipped"; "processing")}}.
```

## Function Categories

For complete function signatures and examples, read `references/functions-reference.md`.
For date/time formatting and parsing tokens, read `references/datetime-tokens.md`.

### General Functions
Core logic and data access: `get`, `if`, `ifempty`, `switch`, `omit`, `pick`.

### Math Functions
Numeric operations: `abs`, `average`, `ceil`, `floor`, `formatNumber`, `max`, `median`, `min`, `parseNumber`, `round`, `stdevp`, `stdevs`, `sum`, `trunc`. Variable: `random`.

### Text and Binary Functions
String manipulation: `ascii`, `base64`, `capitalize`, `contains`, `decodeURL`, `encodeURL`, `escapeHTML`, `indexOf`, `length`, `lower`, `md5`, `replace`, `replaceEmojiCharacters`, `sha1`, `sha256`, `sha512`, `split`, `startCase`, `stripHTML`, `substring`, `toBinary`, `toString`, `trim`, `upper`.

### Date and Time Functions
Date operations: `formatDate`, `parseDate`, `addDays`, `addHours`, `addMinutes`, `addMonths`, `addSeconds`, `addYears`, `setSecond`, `setMinute`, `setHour`, `setDay`, `setDate`, `setMonth`, `setYear`. Variable: `now`.

### Array Functions
Array operations: `add`, `contains`, `deduplicate`, `distinct`, `first`, `flatten`, `join`, `keys`, `last`, `length`, `map`, `merge`, `remove`, `reverse`, `shuffle`, `slice`, `sort`, `toArray`, `toCollection`.

## Common Patterns and Recipes

### Conditional with fallback
```
{{ifempty(1.nickname; 1.firstName)}}
```

### Nested conditionals
```
{{if(1.score > 90; "A"; if(1.score > 80; "B"; if(1.score > 70; "C"; "F")))}}
```

### Switch for multiple values
```
{{switch(1.status; "active"; "✅ Active"; "paused"; "⏸ Paused"; "cancelled"; "❌ Cancelled"; "Unknown")}}
```

### Extract from nested JSON
```
{{get(1.data; "results.0.address.city")}}
```
Note: Inside `get()`, array indices start at 0 in the path string, but standalone array references use index 1.

### Format phone number
```
{{if(contains(1.phone; "+"); 1.phone; "+1" + replace(1.phone; /[^0-9]/g; ""))}}
```

### Calculate days between dates
```
{{round((2.value - 1.value) / 1000 / 60 / 60 / 24)}}
```
Both values must be Date type. Use `parseDate()` to convert strings first.

### Get last day of previous month
```
{{addDays(setDate(now; 1); -1)}}
```

### Transform seconds to HH:MM:SS
```
Hours: {{floor(1.seconds / 3600)}}
Minutes: {{floor((1.seconds % 3600) / 60)}}
Seconds: {{(1.seconds % 3600) % 60}}
```

### Build comma-separated list from array
```
{{join(map(1.items[]; "name"); ", ")}}
```

### Filter and extract from complex array
```
{{map(1.contacts[]; "email"; "type"; "work")}}
```
Returns only emails where type = "work".

### Base64 encode/decode
```
Encode: {{base64(1.text)}}
Decode: {{toString(toBinary(1.base64String; "base64"))}}
```

### Generate HMAC signature
```
{{sha256(1.payload; "hex"; 1.secretKey)}}
```

### Regex replace with capture group
```
{{replace(1.text; /(\d{3})(\d{3})(\d{4})/; "($1) $2-$3")}}
```
**WARNING:** Named capture groups (`(?<n>...)`) are NOT supported and will throw an error.

### Random integer in range
```
{{floor(random * (100 - 1 + 1)) + 1}}
```

## Common Mistakes to Prevent

1. **Using commas instead of semicolons** — Always `;` between parameters
2. **Using JavaScript methods** — No `.toLowerCase()`, `.split()`, `.includes()` etc.
3. **Using `===` or `==`** — Make uses single `=` for equality
4. **Using `? :` ternary** — Use `if(condition; true; false)` instead
5. **Using `&&` / `||`** — Use `and` / `or` keywords
6. **Array index 0** — Make arrays start at index **1** (except inside `get()` path strings and `slice()`)
7. **Using `null`/`undefined`** — Use `ifempty()` to check for empty values
8. **Forgetting `{{ }}`** — All expressions need double curly braces in mapping fields
9. **Using `new Date()`** — Use `now` variable or `parseDate()` function
10. **Using `JSON.parse()`/`JSON.stringify()`** — Use Make's built-in JSON module or `toString()`/`toBinary()`
11. **Named regex capture groups** — Only positional `$1`, `$2` etc. work in `replace()`
12. **Using `.length`** — Use `length(array)` or `length(text)` function instead

## Built-in Modules vs Functions

Make has built-in **modules** (Tools, JSON, etc.) and built-in **functions** (what this skill covers). Do not confuse them:

- **Functions** go in mapping fields inside `{{ }}` — e.g., `{{lower(1.name)}}`
- **Modules** are separate steps in the scenario — e.g., JSON > Parse JSON, Tools > Set Variable
- The **JavaScript module** (Tools > Run JavaScript) does accept real JavaScript, but it's a separate execution context and has its own operation cost
- Custom functions (Enterprise only) are written in JavaScript but called like built-in functions

## Operators Reference

| Operator | Description |
|----------|-------------|
| `+` | Addition / string concatenation |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Division |
| `%` | Modulo |
| `=` | Equal to |
| `!=` | Not equal to |
| `<` | Less than |
| `>` | Greater than |
| `<=` | Less than or equal |
| `>=` | Greater than or equal |
| `and` | Logical AND |
| `or` | Logical OR |
| `not` | Logical NOT |