# 2️⃣ Core Syntax Rules (Yeh Sabse Important Hai)
Rule 1: Indentation matters (Spaces, TABS NAHI)
parent:
  child: value

Har level pe 2 spaces indent karna standard practice hai
TAB key kabhi use mat karna - YAML parser TAB ko reject karega ya error dega
Same level ke items ka indentation exactly same hona chahiye

# Rule 2: Key-Value Pairs
name: Kaif
college: Bright Jr College
age: 20

key: value format
Colon : ke baad ek space zaroor do, warna parser confuse ho jayega
name:Kaif (galat) vs name: Kaif (sahi)

# Rule 3: Lists/Arrays (dash - se banti hain)
skills:
  - Docker
  - Kubernetes
  - Ansible
Ya inline (flow style) me:
skills: [Docker, Kubernetes, Ansible]

# Rule 4: Nested Objects (Maps ke andar Maps)
student:
  name: Kaif
  college: Bright Jr College
  courses:
    - name: Docker
      duration: 4 weeks
    - name: Kubernetes
      duration: 6 weeks
Yahan courses ek list hai, aur us list ka har item khud ek map hai (name aur duration).

# Rule 5: Strings
message1: Hello World          # bina quotes ke bhi chalega
message2: "Hello World"        # double quotes
message3: 'Hello World'        # single quotes
Quotes tab zaroori hote hain jab:

String me special characters ho (:, #, @)
String number jaisa dikhta ho but text treat karna ho: version: "3.8"

# Rule 6: Multi-line strings
description: |
  Yeh line 1 hai
  Yeh line 2 hai
  Newlines preserve honge

summary: >
  Yeh line 1 hai
  Yeh line 2 hai
  Sab ek line me fold ho jayega

| (pipe) = literal block, line breaks preserve hote hain
> (folded) = line breaks spaces me convert ho jate hain

# Rule 7: Comments
-# Yeh ek comment hai, parser ignore karega
name: Kaif  # inline comment bhi chal jayega

# Rule 8: Boolean, Null, Numbers
is_active: true
is_deleted: false
value: null        # ya ~ bhi likh sakte ho
count: 42
price: 19.99

# Rule 9: Multiple documents in one file
---
name: doc1
---
name: doc2

Teen dashes (---) se ek file me multiple YAML documents separate hote hain (Kubernetes me common hai jab ek file me multiple resources define karte ho).


# 3️⃣ Line-by-Line Breakdown - Ek Real Example (Docker Compose)
version: "3.8"
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    environment:
      - ENV=production
    depends_on:
      - db
  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: secret123

# Line by line:
- version: "3.8" → Docker Compose file format ka version bata rahe hain. Quotes me isliye kyunki "3.8" ko string treat karna hai, number nahi.
- services: → Top-level key, iske andar saare containers define honge. Colon ke baad kuch value nahi, matlab uske andar nested block aayega.
- web: → Ek service ka naam (indented under services), yeh container ka logical name hai.
- image: nginx:latest → Yeh service kaunsi Docker image use karegi.
- ports: → List start ho rahi hai (nested key with no direct value)
- "80:80" → Host port 80 ko container port 80 se map kar rahe hain. Quotes isliye kyunki colon : special character hai.
- environment: → Environment variables ki list
- depends_on: → Yeh service kis service pe depend karti hai (db pehle start hogi)
- db: → Doosri service, same indentation level pe web ke jitni (sibling)

Agar tum indentation break karo (jaise image ko web ke barabar laa do instead of nested), poora structure hierarchy change ho jayega aur parser error dega ya galat meaning nikalega.


# 6️⃣ Execution Flow (Kaise Process Hota Hai)

1. Tum YAML file likhte ho
2. Tool (Docker, Kubernetes, Ansible, CI runner) us file ko parse karta hai - YAML parser use hota hai (jaise PyYAML Python me)
3. Parser YAML ko internally key-value data structure (dictionary/hashmap) me convert karta hai
4. Wo tool us data structure ko read karke actual actions perform karta hai (container start karo, pod deploy karo, pipeline steps chalao)

Matlab YAML sirf data represent karta hai, khud execute nahi hota - yeh executable code nahi, configuration hai.