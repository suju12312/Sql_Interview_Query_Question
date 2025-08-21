# SQL Interview Questions - Set 2

## EmployeeDetail Table



| S.No | EmployeeID | FirstName | LastName | Salary |
| ---- | ---------- | --------- | -------- | ------ |
| 1    | 1          | Nitesh    | Amloat   | 6000   |
| 2    | 2          | Nikita    | Jain     | 5300   |
| 3    | 3          | Ashish    | Kumar    | 10000  |
| 4    | 4          | Sujal     | Gupta    | 48000  |
| 5    | 5          | Shubham   | Jaiswal  | 50000  |

| Joining Date        | Department | Gender |
| ------------------- | ---------- | ------ |
| 2013-02-15 11:16:28 | IT         | Male   |
| 2014-01-29 17:31:07 | HR         | Female |
| 2014-01-09 10:05:07 | IT         | Male   |
| 2014-01-09 09:00:07 | HR         | Male   |
| 2014-01-05 05:33:07 | Payroll    | Male   |

---

## Question 1  
**📝 Problem:** 
Boss bolta hai: "Mujhe un employees ka detail do jinka first name A se P ke beech start nahi hota hai."

Tumhare mind me turant aaya → "NOT LIKE [A-P]%" lagana padega.

**🧠 Explanation (Hinglish):**

LIKE '[A-P]%' → naam A se P ke letters se start hote hain.
NOT LIKE '[A-P]%' → matlab unko exclude kardo.
% → baad me kuch bhi ho sakta hai.

**✅ Solution:**
```sql
SELECT * 
FROM EmployeeDetail
WHERE FirstName NOT LIKE '[A-P]%';
```
**📊 Output:**
| EmployeeID | FirstName | LastName | Salary | Joining Date        | Department | Gender |
| ---------- | --------- | -------- | ------ | ------------------- | ---------- | ------ |
| 4          | Sujal     | Gupta    | 48000  | 2014-01-09 09:00:07 | HR         | Male   |
| 5          | Shubham   | Jaiswal  | 50000  | 2014-01-05 05:33:07 | Payroll    | Male   |

---

## Question 1  
**📝 Problem:** 
Boss bolta hai: "Mujhe un employees ka detail do jinka first name A se P ke beech start nahi hota hai."

Tumhare mind me turant aaya → "NOT LIKE [A-P]%" lagana padega.

**🧠 Explanation (Hinglish):**

LIKE '[A-P]%' → naam A se P ke letters se start hote hain.
NOT LIKE '[A-P]%' → matlab unko exclude kardo.
% → baad me kuch bhi ho sakta hai.

**✅ Solution:**
```sql
SELECT * 
FROM EmployeeDetail
WHERE FirstName NOT LIKE '[A-P]%';
```
**📊 Output:**
| EmployeeID | FirstName | LastName | Salary | Joining Date        | Department | Gender |
| ---------- | --------- | -------- | ------ | ------------------- | ---------- | ------ |
| 4          | Sujal     | Gupta    | 48000  | 2014-01-09 09:00:07 | HR         | Male   |
| 5          | Shubham   | Jaiswal  | 50000  | 2014-01-05 05:33:07 | Payroll    | Male   |


---



## Question 2
**📝 Problem:** 
Boss bolta hai: "Mujhe gender column me wo value do jo ‘le’ pe end ho aur total 4 letters ho."

Tum sochte ho — "__le" use karenge (underscore ek character match karta hai).

**🧠 Explanation (Hinglish):**

_ (underscore) → exactly ek single character ko match karega.

__le → total 4 characters (pehle 2 kuch bhi ho sakte hain, last 2 fix 'le').

Yaha pe ‘Male’ aur ‘Female’ check hoga, lekin Female ka length 6 hai isliye nahi aayega.

**💡 Mind Trick:**

% → “kitne bhi characters” (0 or more).
_ → “ek exact character”.
Jab tumhe exact length control karna ho, _ use karo.

✅ Solution:
```sql
SELECT Gender
FROM EmployeeDetail
WHERE Gender LIKE '__le';

```
**📊 Output:**
| Gender |
| ------ |
| Male   |
| Male   |
| Male   |
| Male   |


---
## Question 3
**📝 Problem:** 
Boss bolta hai: "Mujhe wo employees chahiye jinka FirstName ‘A’ se start hota hai aur total 5 letters ka hota hai."

Tum sochte ho — "__le" use karenge (underscore ek character match karta hai).

**🧠 Explanation (Hinglish):**
LIKE 'A____' → ek ‘A’ + 4 underscore → total 5 characters.

_ (underscore) → ek character compulsory.

**💡 Mind Trick:**

A% → sab A se start hone wale.
A____ → sirf 5-letter wale names.
Underscore = tumhari “length wali filter machine”.

**✅ Solution:**
```sql
SELECT * 
FROM EmployeeDetail
WHERE FirstName LIKE 'A____';


```
**📊 Output:**
| EmployeeID | FirstName | LastName | Salary | Joining Date        | Department | Gender |
| ---------- | --------- | -------- | ------ | ------------------- | ---------- | ------ |
| 3          | Ashish    | Kumar    | 10000  | 2014-01-09 10:05:07 | IT         | Male   |


---
## Question 4
**📝 Problem:** 
Boss bolta hai: "Mujhe wo employees do jinke FirstName me % (percentage sign) character ho."
Tum sochte ho — “Arre, % to SQL me wildcard hai… isko search karne ke liye ESCAPE use karna padega.”

**🧠 Explanation (Hinglish):**
% → normally wildcard hota hai (0 ya zyada characters match karta hai).
Agar tumhe literally % character search karna hai → LIKE '%[%]%'.
Bracket [%] → literal percent ko treat karta hai.

**💡 Mind Trick:**
Normal % = wildcard.
Agar tumhe literal % ya _ search karna hai → use [] brackets.
[ % ] ya [ _ ] = exact character search.

**✅ Solution:**
```sql
SELECT * 
FROM EmployeeDetail
WHERE FirstName LIKE '%[%]%';
```
**📊 Output:**
⚠️ Current table me koi bhi naam me % nahi hai → result empty aayega.

---
## Question 5
**📝 Problem:** 
Boss bolta hai: "Mujhe company ke sab unique departments ki list chahiye, duplicate nahi."

Tum sochte ho — "DISTINCT" ka use karenge.

**🧠 Explanation (Hinglish):**
DISTINCT → duplicate values ko remove karta hai.

Isse tumhe sirf ek-ek department ka naam milega.

**💡 Mind Trick:**
DISTINCT = "Unique banane ki machine".

Jab kabhi duplicate remove karna ho → DISTINCT yaad rakhna.
**✅ Solution:**
```sql
SELECT DISTINCT Department 
FROM EmployeeDetail;

```
**📊 Output:**
| Department |
| ---------- |
| IT         |
| HR         |
| Payroll    |

---
## Question 6
**📝 Problem:** 
Boss bolta hai: "Mujhe company me sabse highest salary batao."

Tumhare dimaag me aaya → "MAX()" use karenge.

**🧠 Explanation (Hinglish):**
MAX(Salary) → ek aggregate function hai jo column me sabse badi value return karta hai.

Yaha pe max salary 50,000 hogi.

**💡 Mind Trick:**
MAX() → sabse bada.

MIN() → sabse chhota.

Ye dono column ka scan karke ek single value return karte hain.
**✅ Solution:**
```sql
SELECT MAX(Salary) AS HighestSalary
FROM EmployeeDetail;
```
**📊 Output:**
| HighestSalary |
| ------------- |
| 50000         |

---
## Question 7
**📝 Problem:** 
Boss bolta hai: "Mujhe lowest salary bhi batao."

Tum sochte ho → "MIN()" ka use karenge.

**🧠 Explanation (Hinglish):**
MIN(Salary) → sabse chhoti value nikal ke dega.

Table me sabse lowest salary 5300 hai.

**💡 Mind Trick:**
MAX() aur MIN() dono opposite twins hai.

Ek maximum value nikalta hai, doosra minimum.

**✅ Solution:**
```sql
SELECT MIN(Salary) AS LowestSalary
FROM EmployeeDetail;

```
**📊 Output:**
| LowestSalary |
| ------------ |
| 5300         |



---
## Question 8
**📝 Problem:** 
Boss bolta hai: "Mujhe JoiningDate ko dd mon yyyy format me chahiye (jaise 15 Feb 2013)."

Tum sochte ho — "CONVERT" use karenge.

**🧠 Explanation (Hinglish):**
SQL Server me CONVERT() date/time ka format change karne ke liye use hota hai.

CONVERT(VARCHAR(20), JoiningDate, 106)

VARCHAR(20) → output string max 20 characters.

JoiningDate → column name.

106 → style code jo dd mon yyyy format deta hai.

**💡 Mind Trick:**
Date format badalne ka kaam → CONVERT() ya FORMAT().

Style codes yaad rakhne ki zarurat nahi, Google hi tumhara dost hai 😅

**✅ Solution:**
```sql
SELECT CONVERT(VARCHAR(20), JoiningDate, 106) AS FormattedDate
FROM EmployeeDetail;

```
**📊 Output:**
| FormattedDate |
| ------------- |
| 15 Feb 2013   |
| 29 Jan 2014   |
| 09 Jan 2014   |
| 09 Jan 2014   |
| 05 Jan 2014   |

---
## Question 9
**📝 Problem:** 
Boss bolta hai: "Mujhe JoiningDate ko yyyy/mm/dd format me chahiye (jaise 2013/02/15)."

Tum sochte ho — "CONVERT" use karenge lekin style code change karna hoga.

**🧠 Explanation (Hinglish):**
CONVERT(VARCHAR(20), JoiningDate, 111)

111 → ISO format deta hai (yyyy/mm/dd).

Yeh format reporting ke liye zyada use hota hai.

**💡 Mind Trick:**
106 → dd mon yyyy

111 → yyyy/mm/dd

Bas yaad rakho: style code hi format decide karta hai.

**✅ Solution:**
```sql
SELECT CONVERT(VARCHAR(20), JoiningDate, 111) AS FormattedDate
FROM EmployeeDetail;
```
**📊 Output:**
| FormattedDate |
| ------------- |
| 2013/02/15    |
| 2014/01/29    |
| 2014/01/09    |
| 2014/01/09    |
| 2014/01/05    |


---
## Question 10
**📝 Problem:** 
Boss bolta hai: "Mujhe sirf JoiningDate ka time part chahiye, date nahi."

Tum sochte ho — "CONVERT" ka style code use karenge jo sirf time return kare.

**🧠 Explanation (Hinglish):**
CONVERT(VARCHAR(20), JoiningDate, 108)

108 → style code jo time deta hai format hh:mm:ss.

Date part hata ke sirf time dikhata hai.

**💡 Mind Trick:**
Agar date format chahiye → alag style codes (106, 111, etc).

Agar sirf time chahiye → style 108 yaad rakho (time-only).

**✅ Solution:**
```sql
SELECT CONVERT(VARCHAR(20), JoiningDate, 108) AS TimeOnly
FROM EmployeeDetail;
```
**📊 Output:**
| TimeOnly |
| -------- |
| 10:00:00 |
| 09:00:00 |
| 10:05:07 |
| 10:05:07 |
| 09:00:00 |


**---------------------------Set 2 complete-----------------------------------------------------------------------------**
