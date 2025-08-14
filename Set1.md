# SQL Interview Questions - Set 1

## EmployeeDetail Table

| S.No | EmployeeID | FirstName | LastName | Salary |
|------|------------|-----------|----------|--------|
| 1    | 1          | Nitesh    | Amloat   | 6000   |
| 2    | 2          | Nikita    | Jain     | 5300   |
| 3    | 3          | Ashish    | Kumar    | 10000  |
| 4    | 4          | Sujal     | Gupta    | 48000  |
| 5    | 5          | Shubham   | Jaiswal  | 50000  |

| Joining Date       | Department | Gender |
|--------------------|------------|--------|
| 2013-02-15 11:16:28| IT         | Male   |
| 2014-01-29 17:31:07| HR         | Female |
| 2014-01-09 10:05:07| IT         | Male   |
| 2014-01-09 09:00:07| HR         | Male   |
| 2014-01-05 05:33:07| Payroll    | Male   |

---

## Question 1  
**📝 Problem:**  
Imagine karo tum HR ho aur tumhe **poore company ke employees ka full detail** chahiye — naam, salary, department… sab kuch!  
Boss ne bola: *"Mujhe abhi chahiye, warna bonus cancel!"* 😅  
Tumhare dimaag me turant aaya — *"Bas SELECT * maarte hain, easy job."*

**🧠 Explanation (Hinglish):**  
- `SELECT *` → iska matlab hai **sabhi columns lao**.  
- `FROM EmployeeDetail` → bata raha hai kaunsa table target hai.  
- Output me tumhe poora table waise ka waise mil jayega.

💡 **Mind Trick:** Query likhne se pehle apne aap se poochho — *"Main ye query kisi ko 1 sentence me samjha sakta hoon?"*  
Agar haan, to tum query samajh chuke ho.

**✅ Solution:**
```sql
SELECT * FROM EmployeeDetail;
```

**📊 Output:**
| EmployeeID | FirstName | LastName | Salary | Joining Date       | Department | Gender |
|------------|-----------|----------|--------|--------------------|------------|--------|
| 1          | Nitesh    | Amloat   | 6000   | 2013-02-15 11:16:28| IT         | Male   |
| 2          | Nikita    | Jain     | 5300   | 2014-01-29 17:31:07| HR         | Female |
| 3          | Ashish    | Kumar    | 10000  | 2014-01-09 10:05:07| IT         | Male   |
| 4          | Sujal     | Gupta    | 48000  | 2014-01-09 09:00:07| HR         | Male   |
| 5          | Shubham   | Jaiswal  | 50000  | 2014-01-05 05:33:07| Payroll    | Male   |

---

## Question 2  
**📝 Problem:**  
Boss bolta hai: *"Mujhe sirf employees ka first name chahiye, pura table nahi."*  
Tum sochte ho — *"Arre, ye toh easy hai, ek hi column select karna hai."*

**🧠 Explanation (Hinglish):**  
- `SELECT FirstName` → sirf **FirstName column** laata hai.  
- `FROM EmployeeDetail` → table ka naam jahan se data fetch karna hai.  

💡 **Mind Trick:** Query ko ek shopping list samjho — jitna chahiye sirf wahi likho, sab kuch mat uthao.

**✅ Solution:**
```sql
SELECT FirstName 
FROM EmployeeDetail;
```
**📊 Output:**
| FirstName |
| --------- |
| Nitesh    |
| Nikita    |
| Ashish    |
| Sujal     |
| Shubham   |

---

## Question 3  
**📝 Problem:**  
Boss ka phone aaya 📞:  
*"Mujhe employee ke naam sab **CAPITAL LETTERS** me chahiye, taaki presentation me smart lage."*  
Tumne socha — *"Bas `UPPER()` lagana padega."*  

**🧠 Explanation (Hinglish):**  
- `UPPER(FirstName)` → jo bhi naam hoga, uske **saare letters capital** me convert ho jayenge.  
- `AS 'First Name'` → output column ka naam set karta hai.  
- `FROM EmployeeDetail` → table ka source data.  

💡 **Mind Trick:**  
- `UPPER()` → All caps.  
- `LOWER()` → All small.  

**✅ Solution:**
```sql
SELECT UPPER(FirstName) AS "First Name" 
FROM EmployeeDetail;
```

**📊 Output:**
| First Name |
| ---------- |
| NITESH     |
| NIKITA     |
| ASHISH     |
| SUJAL      |
| SHUBHAM    |

---

## Question 4  
**📝 Problem:**  
Boss bolta hai: *"Ab wahi first names **small letters** me dikhao, email-list jaise."* ✉️  
Tum sochte ho — *"`LOWER()` se ho jayega."*

**🧠 Explanation (Hinglish):**  
- `LOWER(FirstName)` → saare letters **lowercase** me convert ho jaate hain.  
- `AS 'First Name'` → output column ka readable naam set karta hai.  
- `FROM EmployeeDetail` → jis table se data aayega.

**✅ Solution:**
```sql
SELECT LOWER(FirstName) AS "First Name"
FROM EmployeeDetail;
```

**📊 Output:**
| First Name |
| ---------- |
| nitesh     |
| nikita     |
| ashish     |
| sujal      |
| shubham    |

---
## Question 5  
**📝 Problem:**  
Boss ne bola: *"First name aur Last name ek hi column me combine karke dikhao, beech me space ke saath."*  
Tum soch rahe ho — *"Bas concat maarte hain, easy!"* 😎

**🧠 Explanation (Hinglish):**  
- `FirstName + ' ' + LastName` → First name, ek space, phir last name.  
- `AS Name` → naya column naam `Name` hoga.  
- MySQL me string combine karne ke liye `CONCAT()` use hota hai.

**✅ Solution (SQL Server / Oracle style):**
```sql
SELECT FirstName + ' ' + LastName AS Name
FROM EmployeeDetail;
```
**📊 Output:**
| EmployeeID | FirstName | LastName | Salary | Joining Date        | Department | Gender |
| ---------- | --------- | -------- | ------ | ------------------- | ---------- | ------ |
| 5          | Shubham   | Jaiswal  | 50003  | 2014-01-05 05:33:07 | Payroll    | Male   |

---
## Question 6  
**📝 Problem:**  
Boss ne bola: *"Employee ka sirf 'Ashish' naam nikal ke do, ya phir uska poora detail dikhado."*  
Tum soch rahe ho — *"Simple WHERE lagana hai."* 😉

**🧠 Explanation (Hinglish):**  
- `WHERE FirstName = 'Ashish'` → filter karega sirf unhi rows ko jinka first name exactly "Vikas" hai.  
- Agar sirf naam chahiye → SELECT me sirf FirstName lo.  
- Agar poora detail chahiye → SELECT * lagao.

**✅ Sirf naam ke liye:**
```sql
SELECT FirstName AS Name
FROM EmployeeDetail
WHERE FirstName = 'Ashish';
```

**📊 Output (Srif naam):**
| Name   |
| ------ |
| Ashish |

**✅ poora detail ke liye:**
```sql
SELECT *
FROM EmployeeDetail
WHERE FirstName = 'Ashish';
```
**📊 Output (Poora detail):**
| EmployeeID | FirstName | LastName | Salary | Joining Date          | Department | Gender |
| ---------- | --------- | -------- | ------ | --------------------- | ---------- | ------ |
| 3          | Ashish    | Kumar    | 10000  | 2014-01-09 10:05:07   | IT         | Male   |


---
## Question 7  
**📝 Problem:**  
Boss ne bola: *"Mujhe un employees ka detail chahiye jinka first name 'A' se start hota hai."*  
Tum soch rahe ho — *"LIKE ka magic lagana padega."* 😉

**🧠 Explanation (Hinglish):**  
- `LIKE 'a%'` → iska matlab hai naam 'A' se shuru hoga, uske baad kuch bhi ho sakta hai.  
- `%` → wildcard hai jo **0 ya zyada characters** ko match karta hai.

**✅ Solution:**
```sql
SELECT *
FROM EmployeeDetail
WHERE FirstName LIKE 'A%';
```
**📊 Output:**
| EmployeeID | FirstName | LastName | Salary | Joining Date        | Department | Gender |
| ---------- | --------- | -------- | ------ | ------------------- | ---------- | ------ |
| 3          | Ashish    | Kumar    | 10000  | 2014-01-09 10:05:07 | IT         | Male   |

---
## Question 8  
**📝 Problem:**  
Boss ne bola: *"Mujhe wo saare employees ka detail do jinke FirstName me kahin bhi 'ik' aata ho."*  
Tumhare dimaag me turant aya — *"Bas `%ik%` laga dete hain, sab match ho jayega!"* 😄

**🧠 Explanation (Hinglish):**  
- `LIKE '%ik%'` → iska matlab hai ki naam ke beech, start ya end me kahin bhi "ik" aa sakta hai.  
- `%` → match karta hai **0 ya zyada characters** ko.  
- Dono taraf `%` lagane se "ik" ke aage ya peeche kuch bhi ho sakta hai.

**✅ Solution:**
```sql
SELECT *
FROM EmployeeDetail
WHERE FirstName LIKE '%ik%';
```

**💡 Trick:**

'ik%' → "ik" se start
'%ik' → "ik" se end
'%ik%' → kahin bhi "ik" ho

**📊 Output:**
| EmployeeID | FirstName | LastName | Salary | Joining Date        | Department | Gender |
| ---------- | --------- | -------- | ------ | ------------------- | ---------- | ------ |
| 2          | Nikita    | Jain     | 5300   | 2014-01-29 17:31:07 | HR         | Female |

---
## Question 9  
**📝 Problem:**  
Boss ne bola: *"Mujhe un employees ka detail chahiye jinka first name 'h' se end hota hai."*  
Tum soch rahe ho — *"LIKE ka magic lagana padega."* 😉

**🧠 Explanation (Hinglish):**  
- `LIKE '%h'` → iska matlab hai naam 'h' se end hoga, uske pahele kuch bhi ho sakta hai.  
- `%` → wildcard hai jo **0 ya zyada characters** ko match karta hai.

**✅ Solution:**
```sql
SELECT *
FROM EmployeeDetail
WHERE FirstName LIKE '%h';
```

**📊 Output:**
| EmployeeID | FirstName | LastName | Salary | Joining Date       | Department | Gender |
|------------|-----------|----------|--------|--------------------|------------|--------|
| 1          | Nitesh    | Amloat   | 6000   | 2013-02-15 11:16:28| IT         | Male   |
| 3          | Ashish    | Kumar    | 10000  | 2014-01-09 10:05:07| IT         | Male   |
---
## Question 10

**📝 Problem:**  
Boss ne bola: *“Mujhe un employees ka detail chahiye jinka **first name A se P ke beech start hota hai**. Jaldi karo, warna report pending!”* 😅  

HR ke dimaag me turant aaya — *"Bas LIKE use karte hain, pattern match karte hain."*

**🧠 Explanation (Hinglish):**  
- `LIKE '[A-P]%'` → matlab: **first letter A se P ke beech ho aur baad me kuch bhi aa sakta hai**.  
- `%` → matlab “baad me koi bhi letters ho sakte hain, mujhe farak nahi padta.”  
- `[A-P]` → matlab **sirf A, B, C…P tak ke letters consider karna**.  

💡 **Mind Trick:** Query likhne se pehle socho — *“Main ye query kisi ko 1 sentence me samjha sakta hoon?”*  
Agar haan, to boss ko report dikhane se pehle tum confident ho.  

**✅ Solution:**
```sql
SELECT *
FROM EmployeeDetail
WHERE FirstName LIKE '[A-P]%';
```

**📊 Output:**
| EmployeeID | FirstName | LastName | Salary | Joining Date        | Department | Gender |
| ---------- | --------- | -------- | ------ | ------------------- | ---------- | ------ |
| 1          | Nitesh    | Amloat   | 6000   | 2013-02-15 11:16:28 | IT         | Male   |
| 2          | Nikita    | Jain     | 5300   | 2014-01-29 17:31:07 | HR         | Female |
| 3          | Ashish    | Kumar    | 10000  | 2014-01-09 10:05:07 | IT         | Male   |





