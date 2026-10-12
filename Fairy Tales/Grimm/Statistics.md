---
tags:
  - grimm
  - index
  - statistics
---

# Statistics

Numbers about the tales and their characters, drawn as charts from `mermaid` code blocks. The character data comes from an AI analysis — see [[Characters]]. Back to the [[Grimm's Household Tales|index]].

## Who Appears

```mermaid
pie showData
    title Characters by kind
    "human" : 839
    "animal" : 194
    "supernatural" : 172
    "collective" : 119
    "personified object" : 30
```

```mermaid
pie showData
    title Good, evil and in between
    "good" : 507
    "neutral" : 420
    "evil" : 215
    "ambivalent" : 212
```

## Good and Evil by Group

Characters per group of tales — the two bars are named series, so they get a legend.

```mermaid
xychart-beta
    title "Good and evil characters"
    x-axis ["Tales of Magic", "Animal Tales", "Jokes and Anecdotes", "Realistic Tales", "Religious Tales"]
    y-axis "Characters"
    bar "Good" [335, 36, 30, 37, 69]
    bar "Evil" [151, 18, 13, 19, 14]
```

## What Happens to Them

```mermaid
xychart-beta horizontal
    title "Events in the life of a character"
    x-axis ["marries", "deceives someone", "dies", "punished", "leaves home", "killed", "reunited", "rescues someone", "transformed", "rewarded", "imprisoned", "deceived", "returns home", "rescued"]
    bar [170, 123, 92, 88, 88, 81, 80, 69, 61, 61, 58, 46, 44, 43]
```

| Event | Characters |
|-------|-----------:|
| 💍 marries | 170 |
| 🦊 deceives someone | 123 |
| ⚰️ dies | 92 |
| ⚖️ punished | 88 |
| 🧳 leaves home | 88 |
| 🗡️ killed | 81 |
| 🤝 reunited | 80 |
| 🦸 rescues someone | 69 |
| 🐸 transformed | 61 |
| 🎁 rewarded | 61 |
| 🔒 imprisoned | 58 |
| 🙈 deceived | 46 |
| 🏠 returns home | 44 |
| 🛟 rescued | 43 |
| 🔓 freed | 43 |
| ⚔️ kills someone | 40 |
| 🌲 abandoned | 36 |
| 💰 becomes rich | 32 |
| ✨ set free from a spell | 22 |
| 👑 becomes king | 20 |
| 🌀 cursed | 17 |
| 💤 falls asleep | 16 |
| ☀️ awakens | 14 |
| 👶 born | 12 |
| 👑 becomes queen | 11 |

## Magic Numbers

In how many tales a number turns up as a motif — three brothers, seven ravens, twelve dancing princesses.

```mermaid
xychart-beta
    title "Tales with this number as a motif"
    x-axis ["two", "three", "four", "five", "six", "seven", "nine", "twelve", "hundred"]
    bar [67, 122, 34, 12, 19, 37, 12, 28, 21]
```

## Length of the Tales

Words per tale, in the order of the collection.

```mermaid
xychart-beta
    title "Words per tale"
    x-axis "Tale" 1 --> 208
    y-axis "Words"
    line [1410, 975, 1899, 3800, 1107, 3128, 1062, 1975, 812, 2420, 1433, 2035, 907, 2946, 1437, 1601, 504, 3061, 3345, 2632, 1147, 629, 1194, 944, 1383, 1263, 738, 2539, 455, 2332, 893, 946, 1332, 774, 3815, 2216, 787, 1173, 1384, 391, 626, 301, 1224, 1614, 1404, 3076, 864, 1987, 1318, 956, 1641, 3102, 2324, 1084, 1479, 3081, 1200, 2573, 8568, 2076, 808, 1016, 1088, 2176, 483, 1084, 799, 937, 982, 2071, 406, 717, 374, 288, 1800, 919, 249, 301, 668, 4142, 981, 2047, 443, 1928, 229, 1729, 2338, 2212, 3091, 1854, 2429, 2261, 1425, 1323, 1440, 2319, 771, 1786, 1263, 1980, 913, 245, 1582, 518, 1398, 4176, 2118, 256, 2349, 396, 3418, 1216, 1750, 142, 1087, 1021, 1165, 2138, 2634, 916, 659, 1248, 1991, 2201, 767, 1663, 2641, 304, 481, 1464, 2706, 1545, 3221, 710, 152, 133, 147, 640, 851, 424, 1296, 168, 1155, 543, 365, 282, 164, 224, 1112, 363, 337, 350, 155, 205, 929, 333, 209, 131, 2435, 252, 2372, 996, 2807, 2632, 256, 458, 1892, 377, 1142, 240, 236, 840, 779, 576, 585, 1439, 3875, 677, 2125, 981, 726, 265, 1265, 2665, 1360, 1099, 376, 181, 1310, 3069, 3823, 240, 1483, 764, 1079, 1977, 1461, 184, 1161, 405, 157, 492, 243, 964, 160, 341, 517, 204]
```

| Longest tales | Words | Shortest tales | Words |
|---------------|------:|----------------|------:|
| [[The Two Brothers]] | 8,568 | [[A Riddling Tale]] | 131 |
| [[The Two Travellers]] | 4,176 | [[The Maid of Brakel]] | 133 |
| [[Brother Lustig]] | 4,142 | [[The Wilful Child]] | 142 |
| [[The Goose-Girl at the Well]] | 3,875 | [[Domestic Servants]] | 147 |
| [[The Drummer]] | 3,823 | [[Knoist and his Three Sons]] | 152 |
| [[The Wishing-Table, the Gold-Ass, and the Cudgel in the Sack]] | 3,815 | [[Brides On Their Trial]] | 155 |
| [[The Story of the Youth Who Went Forth to Learn What Fear Was]] | 3,800 | [[The Rose]] | 157 |
| [[The Two Kings' Children]] | 3,418 | [[Our Lady's Little Glass]] | 160 |

## Most Crowded Tales

| Tale | Characters |
|------|-----------:|
| [[The Story of the Youth Who Went Forth to Learn What Fear Was#Who's Who\|The Story of the Youth Who Went Forth to Learn What Fear Was]] | 18 |
| [[The Two Brothers#Who's Who\|The Two Brothers]] | 15 |
| [[The Singing, Springing Lark#Who's Who\|The Singing, Springing Lark]] | 14 |
| [[The Devil With the Three Golden Hairs#Who's Who\|The Devil With the Three Golden Hairs]] | 13 |
| [[Brother Lustig#Who's Who\|Brother Lustig]] | 13 |
| [[Ferdinand the Faithful#Who's Who\|Ferdinand the Faithful]] | 13 |
| [[The Twelve Idle Servants#Who's Who\|The Twelve Idle Servants]] | 13 |
| [[The Valiant Little Tailor#Who's Who\|The Valiant Little Tailor]] | 12 |
| [[Thumbling as Journeyman#Who's Who\|Thumbling as Journeyman]] | 12 |
| [[Hans in Luck#Who's Who\|Hans in Luck]] | 12 |

## Every Character in One Table

[[All Characters]] lists all characters with every field in one very wide and long table — a good test for printing and PDF export.
