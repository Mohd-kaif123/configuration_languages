# 1. YAML kya hai aur iska purpose
YAML = "YAML Ain't Markup Language" (recursive acronym). Ye ek human-readable data serialization format hai — matlab configuration aur data ko structured tareeke se likhne ka tarika, jise machine bhi easily parse kar sake aur insaan bhi easily padh sake.
JSON aur XML ke comparison me YAML zyada clean dikhta hai kyunki isme curly braces {}, square brackets [], commas — ye sab zaroori nahi hote (though allowed hain). Iski jagah YAML indentation (spacing) aur line breaks use karta hai structure define karne ke liye.


# 2. Core Syntax Rules (ye sabse important hai — line by line samjho)
# Rule 1: Indentation matters (spaces, not tabs!)
person:
  name: Kaif
  college: Bright Jr College

Har nested level 2 spaces se indent hota hai (convention hai, but consistent hona chahiye).
TAB kabhi use mat karo — YAML parser tab ko reject kar dega ya error dega. Ye sabse common beginner mistake hai.
Indentation hi batata hai ki kaunsa key kiske andar (child) hai.


# Rule 2: Key-Value pairs
name: Kaif
age: 20
is_student: true

Syntax: key: value — colon ke baad ek space zaroori hai.
name:Kaif (bina space) — ye invalid hai, error aayega.
name: Kaif (space ke saath) — ye valid hai.


# Rule 3: Lists / Arrays
skills:
  - Docker
  - Kubernetes
  - Linux

Dash (-) ke baad space, phir value.
Ye ek array hai: ["Docker", "Kubernetes", "Linux"]

Inline (flow style) me bhi likh sakte ho:
skills: [Docker, Kubernetes, Linux]


# Rule 4: Nested structures (maps of maps, lists of maps)
yamlstudents:
  - name: Kaif
    course: DevOps
  - name: Rahul
    course: Cloud
Ye ek list of dictionaries hai — real projects (like GitHub Actions, Kubernetes) me ye pattern bahut use hota hai.


# Rule 5: Data types
string_value: "Hello World"      # string (quotes optional)
number_value: 42                 # integer
float_value: 3.14                # float
boolean_value: true              # boolean (true/false, yes/no bhi chalta hai)
null_value: null                 # null (ya ~ bhi use hota hai)

# Rule 5: Data types

| Key / Syntax | Data Type | Description / Sub-rules |
| :--- | :--- | :--- |
| `string_value: "Hello World"` | **String** | Quotes (`" "` ya `' '`) optional hote hain, par special characters hon toh quotes zaroori hain. |
| `number_value: 42` | **Integer** | Normal whole numbers (positive ya negative). |
| `float_value: 3.14` | **Float** | Decimal wale numbers. |
| `boolean_value: true` | **Boolean** | `true`/`false` use hota hai (kuch parsers me `yes`/`no` ya `on`/`off` bhi chal jata hai). |
| `null_value: null` | **Null** | Empty value ke liye `null` likhte hain, ya fir sirf tilde (`~`) sign bhi use kar sakte hain. |

# Rule 6: Multi-line strings
yamldescription: |
  Ye pehli line hai.
  Ye doosri line hai.
  Line breaks preserve honge.

summary: >
  Ye text ek single
  line me fold ho jayega
  spaces ke saath.

| (pipe) → literal block — line breaks as-it-is rehte hain.
> (folded) → line breaks spaces me convert ho jaate hain (paragraph jaisa).

# Rule 7: Comments
Ye ek comment hai
name: Kaif  # inline comment bhi chalta hai

Rule 8: Anchors & Aliases (reusability ke liye — advanced but interview me pucha jata hai)
yamldefault_config: &defaults
  timeout: 30
  retries: 3

service_a:
  <<: *defaults
  name: ServiceA

&defaults → ek anchor banata hai (ek block ko naam de rahe ho)
*defaults → us anchor ko reference/reuse karta hai
<<: → merge key hai (defaults ko yaha inject kar diya)

Ye Docker Compose aur Kubernetes me DRY (Don't Repeat Yourself) ke liye use hota hai.

# 3. Effect of breaking rules (galti karoge to kya hoga)
> Galti                                       Result
- Tab use karna indentation ke liye           Parser error: "found character that cannot start any token"
- Colon ke baad space missing                 Parsing error ya value galat interpret hoga
- Inconsistent indentation (kabhi 2,4 space)  YAMLError: bad indentation
- Dash ke baad space missing (-item)          List item properly parse nahi hoga  
- Special characters (:, #, {, }) bina        Unexpected parsing behavior
  quotes ke string me                         


# Table:-
# 3. Effect of breaking rules (galti karoge to kya hoga)

| Galti | Result |
| :--- | :--- |
| **Tab use karna indentation ke liye** | Parser error: `"found character that cannot start any token"` |
| **Colon ke baad space missing** | Parsing error ya value galat interpret hoga |
| **Inconsistent indentation (kabhi 2, kabhi 4 space)** | `YAMLError: bad indentation` |
| **Dash ke baad space missing (`-item`)** | List item properly parse nahi hoga |
| **Special characters (`:`, `#`, `{`, `}`) bina quotes ke string me** | Unexpected parsing behavior |