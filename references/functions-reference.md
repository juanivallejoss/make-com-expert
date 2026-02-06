# Make.com Functions Complete Reference

> Source: https://help.make.com/functions (Jan 2026)

## Table of Contents

1. [General Functions](#general-functions)
2. [Math Functions](#math-functions)
3. [Math Variables](#math-variables)
4. [Text and Binary Functions](#text-and-binary-functions)
5. [Date and Time Functions](#date-and-time-functions)
6. [Array Functions](#array-functions)

---

## General Functions

### get
`get(object or array; path)`
Returns the value at path of an object or array. Use dot notation for nested objects. **First item in array is index 1** (not 0).
```
get(array; 1+1)
get(array; 5.raw_name)
get(object; raw_name)
get(object; raw_name.sub_raw_name)
```

### if
`if(expression; value1; value2)`
Returns value1 if expression is true; otherwise value2.
```
if(1=1; a; b) = a
if(1=2; a; b) = b
```

### ifempty
`ifempty(value1; value2)`
Returns value1 if not empty; otherwise value2.
```
ifempty(a; b) = a
ifempty(unknown; b) = b
ifempty(""; b) = b
```

### switch
`switch(expression; value1; result1; [value2; result2; ...]; [else])`
Evaluates expression against a list of values, returns the result of the first match.
```
switch(b; a; 1; b; 2; c; 3) = 2
switch(c; a; 1; b; 2; c; 3) = 3
switch(x; a; 1; b; 2; c; 3; 4) = 4
```

### omit
`omit(collection; key1; [key2; ...])`
Removes specified keys from a collection. Returns collection with remaining elements.

### pick
`pick(collection; key1; [key2; ...])`
Picks only specified keys from a collection. Returns collection with only picked elements.

---

## Math Functions

### abs
`abs(number)`
Returns absolute value.
```
abs(-5) = 5
abs(3.7) = 3.7
```

### average
`average([array of values])` or `average(value1; [value2]; ...)`
Returns average of numeric values in an array or entered individually.

### ceil
`ceil(number)`
Returns smallest integer >= number.
```
ceil(1.2) = 2
ceil(4) = 4
```

### floor
`floor(number)`
Returns largest integer <= number.
```
floor(1.2) = 1
floor(1.9) = 1
```

### formatNumber
`formatNumber(number; decimalPoints; [decimalSeparator]; [thousandsSeparator])`
Formats a number. Default decimal separator is `,`, default thousands separator is ` ` (space).
```
formatNumber(123456789; 3; ,; .) = 123.456.789,000
```

### max
`max([array of values])` or `max(value1; value2; ...)`
Returns largest number.

### median
`median([array of values])`
Returns median value.
```
median(3; 5; 7) = 5
median(2; 3; 5; 8) = 4
```

### min
`min([array of values])` or `min(value1; value2; ...)`
Returns smallest number.

### parseNumber
`parseNumber(number; decimalSeparator)`
Parses a string with a number and returns the number.
```
parseNumber(1.756,456; ,) = 1756.456
```

### round
`round(number)`
Rounds to nearest integer.
```
round(1.2) = 1
round(1.5) = 2
```

### stdevp
`stdevp([array of values])`
Returns standard deviation of population values.
```
stdevp(1; 2; 3; 4; 5) = 1.4142135623730951
```

### stdevs
`stdevs([array of values])`
Returns standard deviation of sample values.
```
stdevs(1; 2; 3; 4; 5) = 1.5811388300841898
```

### sum
`sum([array of values])` or `sum(value1; value2; ...)`
Returns sum of values.

### trunc
`trunc(number; [precision])`
Truncates a number (removes fractional part). Optional precision parameter.
```
trunc(3.789) = 3
trunc(3.789; 2) = 3.78
trunc(3.789; -2) = 3.7
trunc(123.456; -2) = 100
```

---

## Math Variables

### random
`random`
Returns a floating-point pseudo-random number in range [0, 1).

**Generate random integer in range [min, max]:**
```
{{floor(random * (1.max - 1.min + 1)) + 1.min}}
```
**Example (dice roll 1-6):**
```
{{floor(random * 6) + 1}}
```

---

## Text and Binary Functions

### ascii
`ascii(text; [removeDiacritics])`
Removes all non-ASCII characters from text. Set removeDiacritics to `true` to convert accented chars.
```
ascii(Mščařžkýáeíé) = Make
ascii(ěščřž; true) = escrz
```

### base64
`base64(text)`
Transforms text to base64.
```
base64(Make) = TWFrZQ==
```
**Decode base64 to text:**
```
toString(toBinary(TWFrZQ==; base64)) = Make
```

### capitalize
`capitalize(text)`
Converts first character to uppercase.
```
capitalize(make) = Make
```

### contains (string)
`contains(text; searchString)`
Verifies if text contains the search string. Returns true/false.
```
contains(Hello World; Hello) = true
contains(Hello World; Bye) = false
```

### decodeURL
`decodeURL(text)`
Decodes URL-encoded special characters to text.
```
decodeURL(Automate%20your%20workflow) = Automate your workflow
```

### encodeURL
`encodeURL(text)`
Encodes special characters in text to a valid URL address.

### escapeHTML
`escapeHTML(text)`
Escapes all HTML tags in text.
```
escapeHTML(<b>Hello</b>) = &lt;b&gt;Hello&lt;/b&gt;
```

### indexOf
`indexOf(string; value; [start])`
Returns position of first occurrence. Returns -1 if not found.
```
indexOf(Make; k) = 2
indexOf(We love Make; x) = -1
indexOf(We love Make; e; 7) = 11
```

### length (string)
`length(text or buffer)`
Returns length of string (chars) or binary buffer (bytes).
```
length(Hello) = 5
```

### lower
`lower(text)`
Converts all characters to lowercase.
```
lower(Hello) = hello
```

### md5
`md5(text)`
Calculates the MD5 hash of a string.
```
md5(Make) = 529a05ca6c1263aab080ec4f20754411
```

### replace
`replace(text; searchString; replacementString)`
Replaces search string with replacement. Supports regex with flags.
```
replace(Hello World; Hello; Hi) = Hi World
replace(all these numbers 187 23 1 9565 will be replaced with x; /\d+/g; x) = all these numbers x x x x will be replaced with x
```
**Special replacement patterns:**
- `$&` = inserts the matched substring
- `$n` = inserts the nth parenthesized submatch (1-indexed)

```
replace(Phone number is 777111222; /\d+/g; +420$&) = Phone number is +420777111222
replace(Phone number is 777111222; / is (\d)/; +42$1) = Phone number is +420777111222
```
**WARNING:** Do NOT use named capture groups like `/is (?<number>\d+)/` — this throws an error.

### replaceEmojiCharacters
`replaceEmojiCharacters(text)`
Replaces emoji characters with a string representation.

### sha1
`sha1(text; [encoding]; [key])`
Calculates SHA-1 hash. With key, returns HMAC hash. Encodings: `hex` (default), `base64`, `latin1`.

### sha256
`sha256(text; [encoding]; [key]; [keyEncoding])`
Calculates SHA-256 hash. With key, returns HMAC hash. Encodings: `hex` (default), `base64`, `latin1`. Key encodings: `text` (default), `hex`, `base64`, `binary`.

### sha512
`sha512(text; [outputEncoding]; [key]; [keyEncoding])`
Calculates SHA-512 hash. Same encoding options as sha256. When using `binary` key encoding, key must be a buffer, not a string.

### split
`split(text; separator)`
Splits string into array of strings.
```
split(John, George, Paul; ,) = ["John", " George", " Paul"]
```

### startCase
`startCase(text)`
Capitalizes first letter of every word, lowercases all others.
```
startCase(hello WORLD) = Hello World
```

### stripHTML
`stripHTML(text)`
Removes all HTML tags from text.
```
stripHTML(<b>Hello</b>) = Hello
```

### substring
`substring(text; start; end)`
Returns portion of string between start and end positions.
```
substring(Hello; 0; 3) = Hel
substring(Hello; 1; 3) = el
```

### toBinary
`toBinary(value)`
Converts any value to binary data. Optional encoding as second argument: `hex`, `base64`.
```
toBinary(Make) = binary data
```

### toString
`toString(value)`
Converts any value to a string.
```
toString(toBinary(TWFrZQ==; base64)) = Make
```

### trim
`trim(text)`
Removes space characters at start and end of text.

### upper
`upper(text)`
Converts all characters to uppercase.
```
upper(Hello) = HELLO
```

---

## Date and Time Functions

### formatDate
`formatDate(date; format; [timezone])`
Converts a Date value to a text string using format tokens.
```
formatDate(1.dateCreated; MM/DD/YYYY) = 10/01/2018
formatDate(1.dateCreated; YYYY-MM-DD HH:mm A) = 2018-10-01 09:32 AM
formatDate(1.dateCreated; DD.MM.YYYY HH:mm; UTC) = 01.10.2018 07:32
formatDate(now; MM/DD/YYYY HH:mm) = 19/03/2019 15:30
```

### parseDate
`parseDate(text; format; [timezone])`
Converts a text string to a Date value using parsing tokens.
```
parseDate(2016-12-28; YYYY-MM-DD) = 2016-12-28T00:00:00.000Z
parseDate(2016-12-28 16:03; YYYY-MM-DD HH:mm) = 2016-12-28T16:03:00.000Z
parseDate(2016-12-28 04:03 PM; YYYY-MM-DD hh:mm A) = 2016-12-28T16:03:06.000Z
parseDate(1482940986; X) = 2016-12-28T16:03:06.000Z
```

### addDays
`addDays(date; number)`
Returns new date with days added. Negative numbers subtract.
```
addDays(2016-12-08T15:55:57.536Z; 2) = 2016-12-10T15:55:57.536Z
addDays(2016-12-08T15:55:57.536Z; -2) = 2016-12-06T15:55:57.536Z
```

### addHours
`addHours(date; number)`
Returns new date with hours added/subtracted.

### addMinutes
`addMinutes(date; number)`
Returns new date with minutes added/subtracted.

### addMonths
`addMonths(date; number)`
Returns new date with months added/subtracted.

### addSeconds
`addSeconds(date; number)`
Returns new date with seconds added/subtracted.

### addYears
`addYears(date; number)`
Returns new date with years added/subtracted.

### setSecond
`setSecond(date; number)`
Returns new date with seconds set. Accepts 0-59 (overflows to next/prev minute).

### setMinute
`setMinute(date; number)`
Returns new date with minutes set. Accepts 0-59 (overflows to next/prev hour).

### setHour
`setHour(date; number)`
Returns new date with hour set. Accepts 0-23 (overflows to next/prev day).

### setDay
`setDay(date; number/name)`
Sets day of week. Sunday=1, Saturday=7. Accepts English day names.
```
setDay(2018-06-27T11:36:39.138Z; Monday) = 2018-06-25T11:36:39.138Z
setDay(2018-06-27T11:36:39.138Z; 1) = 2018-06-24T11:36:39.138Z
setDay(2018-06-27T11:36:39.138Z; 7) = 2018-06-30T11:36:39.138Z
```

### setDate
`setDate(date; number)`
Sets day of month (1-31, overflows to next/prev month).
```
setDate(2015-08-07T11:36:39.138Z; 5) = 2015-08-05T11:36:39.138Z
setDate(2015-08-07T11:36:39.138Z; 32) = 2015-09-01T11:36:39.138Z
```

### setMonth
`setMonth(date; number/name)`
Sets month (1-12 or English name, overflows to next/prev year).
```
setMonth(2015-08-07T11:36:39.138Z; 5) = 2015-05-07T11:36:39.138Z
setMonth(2015-08-07T11:36:39.138Z; January) = 2015-01-07T12:36:39.138Z
```

### setYear
`setYear(date; number)`
Sets the year.

---

## Array Functions

### add
`add(array; value1; value2; ...)`
Adds values to an array and returns it.

### contains (array)
`contains(array; value)`
Verifies if an array contains the value.

### deduplicate
`deduplicate(array)`
Removes duplicates from an array.

### distinct
`distinct(array; [key])`
Removes duplicates using a key for complex objects. Dot notation for nested properties. Index 1.
```
distinct(Contacts[]; name)
```

### first
`first(array)`
Returns first element.

### flatten
`flatten(array)`
Creates new array with all sub-array elements concatenated recursively.

### join
`join(array; separator)`
Concatenates all items into a string with separator.

### keys
`keys(object)`
Returns array of an object's or array's property names.

### last
`last(array)`
Returns last element.

### length (array)
`length(array)`
Returns number of items.

### map
`map(complexArray; key; [keyForFiltering]; [possibleValuesForFiltering])`
Returns primitive array from complex array values. Allows filtering. Use raw variable names for keys.
```
map(Emails[]; email) — returns array of emails
map(Emails[]; email; label; work,home) — returns emails where label is "work" or "home"
```

### merge
`merge(array1; array2; ...)`
Merges two or more arrays into one.

### remove
`remove(array; value1; value2; ...)`
Removes specified values. Only works on primitive arrays (text/numbers).

### reverse
`reverse(array)`
Reverses array order.

### shuffle
`shuffle(array)`
Randomly reorders elements.

### slice
`slice(array; start; [end])`
Returns new array with selected items. **First item index is 0.**

### sort
`sort(array; [order]; [key])`
Sorts array values.
**Order values:**
- `asc` (default) — ascending
- `desc` — descending
- `asc ci` — case-insensitive ascending
- `desc ci` — case-insensitive descending

Use key for complex objects with dot notation.
```
sort(Contacts[]; name) — ascending by name
sort(Contacts[]; desc; name) — descending by name
sort(Contacts[]; asc ci; name) — case-insensitive ascending
```

### toArray
`toArray(collection)`
Converts a collection into array of key-value collections.

### toCollection
`toCollection(array; key; value)`
Converts an array of key-value objects into a collection.