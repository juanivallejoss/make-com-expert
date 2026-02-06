# Make.com Date/Time Tokens Reference

## Formatting Tokens (for formatDate)

### Year, Month, Day
| Token | Output | Description |
|-------|--------|-------------|
| YY | 70, 71...29, 30 | 2-digit year |
| YYYY | 1970, 1971...2029, 2030 | 4-digit year |
| Y | 1970...9999, +10000 | Year with any digits |
| Q | 1, 2, 3, 4 | Quarter of year |
| Qo | 1st, 2nd, 3rd, 4th | Quarter with ordinal |
| M | 1, 2...11, 12 | Month number |
| Mo | 1st, 2nd...11th, 12th | Month with ordinal |
| MM | 01, 02...11, 12 | Month with leading zero |
| MMM | Jan, Feb...Nov, Dec | Month abbreviation |
| MMMM | January...December | Month full name |
| D | 1, 2...30, 31 | Day of month |
| Do | 1st, 2nd...30th, 31st | Day with ordinal |
| DD | 01, 02...30, 31 | Day with leading zero |
| DDD | 1, 2...364, 365 | Day of year |
| DDDo | 1st...365th | Day of year with ordinal |
| DDDD | 001...365 | Day of year with leading zero |

### Week Year, Week, Weekday
| Token | Output | Description |
|-------|--------|-------------|
| d | 0, 1...5, 6 | Day of week |
| do | 0th, 1st...6th | Day of week with ordinal |
| dd | Su, Mo...Fr, Sa | Day abbreviation (2 char) |
| ddd | Sun, Mon...Fri, Sat | Day abbreviation (3 char) |
| dddd | Sunday...Saturday | Day full name |
| e | 1, 2...6, 7 | Day of week (ISO) |
| w | 1, 2...52, 53 | Week of year |
| wo | 1st...53rd | Week with ordinal |
| ww | 01...53 | Week with leading zero |
| W | 1, 2...52, 53 | Week of year (ISO) |
| Wo | 1st...53rd | Week with ordinal (ISO) |
| WW | 01...53 | Week with leading zero (ISO) |
| gg | 70...30 | Week year |
| gggg | 1970...2030 | Week year (4-digit) |
| GG | 70...30 | Week year (ISO) |
| GGGG | 1970...2030 | Week year (ISO, 4-digit) |

### Hour, Minute, Second, Offset
| Token | Output | Description |
|-------|--------|-------------|
| H | 0...23 | 24-hour time |
| HH | 00...23 | 24-hour with leading zero |
| h | 1...12 | 12-hour time |
| hh | 01...12 | 12-hour with leading zero |
| k | 1...24 | 24-hour (1-indexed) |
| kk | 01...24 | 24-hour (1-indexed) with zero |
| A | AM, PM | Upper case |
| a | am, pm | Lower case |
| m | 0...59 | Minutes |
| mm | 00...59 | Minutes with leading zero |
| s | 0...59 | Seconds |
| ss | 00...59 | Seconds with leading zero |
| S | 0...9 | Fractional seconds |
| SS | 00...99 | Fractional (2 digits) |
| SSS | 000...999 | Milliseconds |
| Z | -07:00...+07:00 | Time zone offset |
| ZZ | -0700...+0700 | Time zone (compact) |
| X | 1360013296 | Unix timestamp (seconds) |
| x | 1360013296123 | Unix timestamp (milliseconds) |

## Parsing Tokens (for parseDate)

### Year, Month, Day
| Token | Example | Description |
|-------|---------|-------------|
| YYYY | 2014 | 4 or 2 digit year |
| YY | 14 | 2-digit year |
| Y | -25 | Year with any digits and sign |
| Q | 1-4 | Quarter (sets month to first of quarter) |
| M, MM | 1-12 | Month number |
| MMM, MMMM | Jan-December | Month name |
| D, DD | 1-31 | Day of month |
| Do | 1st-31st | Day with ordinal |
| DDD, DDDD | 1-365 | Day of year |
| X | 1410715640.579 | Unix timestamp |
| x | 1410715640579 | Unix millisecond timestamp |

### Week, Weekday
| Token | Example | Description |
|-------|---------|-------------|
| ddd, dddd | Mon-Sunday | Day name |
| gggg | 2014 | ISO 4-digit week year |
| gg | 14 | ISO 2-digit week year |
| w, ww | 1-53 | ISO week of year |
| e | 1-7 | ISO day of week |

### Hour, Minute, Second, Offset
| Token | Example | Description |
|-------|---------|-------------|
| H, HH | 0-23 | Hours (24-hour) |
| h, hh | 1-12 | Hours (12-hour, use with A/a) |
| k, kk | 1-24 | Hours (24-hour, 1-indexed) |
| a, A | am, pm | AM/PM |
| m, mm | 0-59 | Minutes |
| s, ss | 0-59 | Seconds |
| S, SS, SSS | 0-999 | Fractional seconds |
| Z, ZZ | +05:30 | UTC offset |