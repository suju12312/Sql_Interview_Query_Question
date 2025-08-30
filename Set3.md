# SQL Interview Questions - Set 3

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

## Question 21  

📝 **Problem:**  
Boss bolta hai: "Mujhe sirf `JoiningDate` ka **Year part** chahiye."

---

🧠 **Explanation (Hinglish):**  
SQL me ek built-in function hota hai → **DATEPART()**  
- Ye function date ke alag-alag parts (Year, Month, Day, Hour, Minute) nikalne ke liye use hota hai.  
- Agar hum `YEAR` pass kare → Sirf year return karega.  

💡 **Mind Trick:**  
- `DATEPART(YEAR, column)` → Year deta hai.  
- `DATEPART(MONTH, column)` → Month deta hai.  
- `DATEPART(DAY, column)` → Day deta hai.  

---

✅ **Solution:**
```sql
SELECT DATEPART(YEAR, JoiningDate) AS JoiningYear
FROM EmployeeDetail;
```

**📊 Output:**
| JoiningYear |
| ----------- |
| 2020        |
| 2021        |
| 2022        |
| 2022        |
| 2021        |

## Question 22  

📝 **Problem:**  
Boss bolta hai: "Mujhe sirf `JoiningDate` ka **Month part** chahiye."

---

🧠 **Explanation (Hinglish):**  
- `DATEPART(MONTH, JoiningDate)` likhne se month ka **numeric value** (1–12) return hota hai.  
- Example: Jan = 1, Feb = 2, Mar = 3 … Dec = 12.  

💡 **Mind Trick:**  
- **YEAR → 2022**  
- **MONTH → 02**  
- **DAY → 15**  

---

✅ **Solution:**
```sql
SELECT DATEPART(MONTH, JoiningDate) AS JoiningMonth
FROM EmployeeDetail;
```
**📊 Output:**
| JoiningMonth |
| ------------ |
| 1            |
| 2            |
| 5            |
| 5            |
| 11           |

---
## Question 23  

📝 **Problem:**  
Boss bolta hai: "System ka current date and time chahiye."  

---

🧠 **Explanation (Hinglish):**  
- `GETDATE()` function system ka current **date + time** return karta hai.  
- Isme date part bhi hota hai aur time part bhi.  

💡 **Mind Trick:**  
- `GETDATE()` = abhi ka live system date & time.  

---

✅ **Solution:**  
```sql
SELECT GETDATE() AS CurrentDateTime;
```

**📊 Output**
2025-08-30 19:20:55.123


---

## Question 24  

📝 **Problem:**  
Boss bolta hai: "Mujhe **UTC time** chahiye, jo time-zone independent ho."  

---

🧠 **Explanation (Hinglish):**  
- `GETUTCDATE()` function **Universal Time (UTC)** deta hai.  
- Ye time **local system time zone se independent** hota hai.  

💡 **Mind Trick:**  
- `GETDATE()` = Local Time  
- `GETUTCDATE()` = UTC / GMT Time  

---

✅ **Solution:**  
```sql
SELECT GETUTCDATE() AS UTCTime;
```
**📊 Output**
2025-08-30 13:50:55.123


---

## Question 25  

📝 **Problem:**  
Boss bolta hai: "Mujhe har employee ka FirstName, Current Date, Joining Date aur dono ke beech difference (in months) chahiye."  

---

🧠 **Explanation (Hinglish):**  
- `DATEDIFF(MM, JoiningDate, GETDATE())` → JoiningDate aur CurrentDate ke beech ka difference **months** me nikalta hai.  
- `MM` specify karta hai ki result **months** me aaye.  

💡 **Mind Trick:**  
- Agar `MM` likha → Difference in **Months**  
- Agar `DD` likha → Difference in **Days**  
- Agar `YY` likha → Difference in **Years**  

---

✅ **Solution:**  
```sql
SELECT FirstName,
       GETDATE() AS CurrentDate,
       JoiningDate,
       DATEDIFF(MM, JoiningDate, GETDATE()) AS TotalMonths
FROM EmployeeDetail;
```

**📊 Output**
FirstName   | CurrentDate          | JoiningDate         | TotalMonths
------------|----------------------|---------------------|------------
Rohit       | 2025-08-30 19:25:00  | 2023-06-15 10:00:00 | 26
Amit        | 2025-08-30 19:25:00  | 2024-01-10 09:00:00 | 19


---

## Question 26  

📝 **Problem:**  
Boss bolta hai: "Mujhe employees ka FirstName, JoiningDate aur abhi tak ka difference (in days) chahiye."  

---

🧠 **Explanation (Hinglish):**  
- `DATEDIFF(DD, JoiningDate, GETDATE())` → Difference ko **days** me return karega.  
- Bas `DD` likhne ka matlab hai → Days count.  

💡 **Mind Trick:**  
- `YY` = Years  
- `MM` = Months  
- `DD` = Days  

---

✅ **Solution:**  
```sql
SELECT FirstName,
       GETDATE() AS CurrentDate,
       JoiningDate,
       DATEDIFF(DD, JoiningDate, GETDATE()) AS TotalDays
FROM EmployeeDetail;
```
**📊 Output**
FirstName   | CurrentDate          | JoiningDate         | TotalDays
------------|----------------------|---------------------|----------
Rohit       | 2025-08-30 19:30:00  | 2025-01-01 09:00:00 | 242
Amit        | 2025-08-30 19:30:00  | 2024-08-15 10:00:00 | 380

## Question 27  

📝 **Problem:**  
Get Employees whose Joining year is **2013**.  

---

🧠 **Explanation (Hinglish):**  
- `DATEPART(YYYY, JoiningDate)` → JoiningDate se **sirf year** nikalta hai.  
- Usko compare karna hai `2013` se.  

💡 **Mind Trick:**  
- `DATEPART(YYYY, column)` = Sirf Year ka part nikalta hai.  

---

✅ **Solution:**  
```sql
SELECT * 
FROM EmployeeDetail
WHERE DATEPART(YYYY, JoiningDate) = 2013;
```
**📊 Output**
EmployeeID | FirstName | JoiningDate
-----------|-----------|-----------------
101        | Rohit     | 2013-05-12
105        | Amit      | 2013-11-30


---

## Question 28  

📝 **Problem:**  
Get Employees whose Joining month is **January**.  

---

🧠 **Explanation (Hinglish):**  
- `DATEPART(MM, JoiningDate)` → JoiningDate se **month number** nikalta hai.  
- `1` means January, `2` means February, etc.  

💡 **Mind Trick:**  
- `MM = 1` → January  
- `MM = 12` → December  

---

✅ **Solution:**  
```sql
SELECT * 
FROM EmployeeDetail
WHERE DATEPART(MM, JoiningDate) = 1;
```
**📊 Output**
EmployeeID | FirstName | JoiningDate
-----------|-----------|-----------------
102        | Suresh    | 2015-01-10
108        | Nidhi     | 2020-01-25


---

## Question 29  

📝 **Problem:**  
Get Employees whose JoiningDate is **between 2013-01-01 and 2013-12-01**.  

---

🧠 **Explanation (Hinglish):**  
- `BETWEEN` operator ek range ke andar values check karta hai.  
- `BETWEEN` inclusive hota hai → Start aur End date dono included hote hain.  

💡 **Mind Trick:**  
- `BETWEEN A AND B` → Includes **A aur B dono**  

---

✅ **Solution:**  
```sql
SELECT * 
FROM EmployeeDetail
WHERE JoiningDate BETWEEN '2013-01-01' AND '2013-12-01';
```
**📊 Output**
EmployeeID | FirstName | JoiningDate
-----------|-----------|-----------------
101        | Rohit     | 2013-03-15
105        | Amit      | 2013-08-20

## Question 30  

📝 **Problem:**  
Count Employees in **EmployeeDetail** table.  

---

🧠 **Explanation (Hinglish):**  
- `COUNT(*)` → Table me total rows count karta hai.  
- `NULL values bhi count hoti hain` kyunki `*` use kar rahe hain.  

💡 **Mind Trick:**  
- `COUNT(*)` = sab count hoga (including NULL)  
- `COUNT(column)` = sirf non-NULL values count hongi.  

---

✅ **Solution:**  
```sql
SELECT COUNT(*) 
FROM EmployeeDetail;
```
**📊 Output**
TotalEmployees
--------------
15

# 📌 Syntax Notes  

---

## 1. DATEPART()

📝 **Syntax:**  
```sql
SELECT DATEPART(part, date) 
FROM TableName;
```

**📌 part options:**

YYYY → Year nikalta hai

MM → Month nikalta hai

DD → Day nikalta hai

HH → Hour nikalta hai

MI → Minute nikalta hai

SS → Second nikalta hai

**🧠 Explanation (Hinglish):**

DATEPART() ek date ke specific part ko nikalta hai.

Example agar date = 2013-05-21, to:

DATEPART(YYYY, date) → 2013

DATEPART(MM, date) → 5 (May)

DATEPART(DD, date) → 21
**✅ Example:**

```sql
SELECT DATEPART(YYYY, JoiningDate) AS Year
FROM EmployeeDetail;
```
**📊 Output**
Year
-----
2013
2015
2020

---
## 2. DATEDIFF()

**📝 Syntax:**

SELECT DATEDIFF(part, start_date, end_date) 
FROM TableName;


**📌 part options:**

YEAR → Saal ka difference

MONTH → Mahine ka difference

DAY → Dinon ka difference

**🧠 Explanation (Hinglish):**

DATEDIFF() do dates ke beech ka difference batata hai.

Pehla date = start date

Doosra date = end date

Result me dono ke beech ka gap aata hai (jaise kitne din / month / saal ka difference hai).

**✅ Example:**

SELECT DATEDIFF(DAY, '2013-01-01', '2013-01-10') AS DaysDiff;


**📊 Output:**

DaysDiff
--------
9
