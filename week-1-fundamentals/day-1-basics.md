# Day 1: Complete Learning Session

**Date:** February 10, 2026  
**Duration:** First study session  
**Status:** ✅ Completed

---

## Hour 1: Apex Fundamentals

### What Is Apex?

Apex is Salesforce's programming language. It lets you tell Salesforce what to do beyond clicking buttons.

**Key Facts:**
- **Strongly typed** - You must declare what type of data each variable holds
- **Object-oriented** - Uses classes and objects (like Java)
- **Server-side** - Runs on Salesforce servers, not your computer
- **Has strict limits** - Governor limits (covered heavily in Week 2)

**Why It's Beginner-Friendly:**
- Syntax similar to Java/C#, but simpler
- You already know Salesforce objects (Account, Contact, etc.)
- Instant feedback in Developer Console

---

### How to Run Apex Code

**Steps:**
1. Login to your Dev Org
2. Click gear icon (⚙️) → Developer Console
3. Go to **Debug → Open Execute Anonymous Window**
4. Paste code and click **Execute**
5. View output in **Logs** tab at the bottom

---

### Example 1: Hello World

```apex
System.debug('Hello, Salesforce Developer!');
```

**What's Happening:**
- `System.debug()` - Prints messages to debug log (like console.log or print)
- `'...'` - Single quotes define text (called a String)
- `;` - Semicolon ends every statement

**✅ Executed Successfully**

---

### Example 2: Variables (Storing Information)

```apex
// Declare variables
String myName = 'John';
Integer myAge = 25;
Boolean isLearning = true;

// Print them
System.debug('Name: ' + myName);
System.debug('Age: ' + myAge);
System.debug('Am I learning Apex? ' + isLearning);
```

**Data Types Learned:**
- `String` - Text (names, emails, addresses)
- `Integer` - Whole numbers (age, count, year)
- `Boolean` - True or false (yes/no questions)
- `//` - Comment (notes for yourself, ignored by Salesforce)
- `+` - Concatenates (combines) text

**✅ Executed Successfully**

---

### Example 3: Working With Salesforce Data

```apex
// Create a new Account
Account myAccount = new Account();
myAccount.Name = 'My First Company';
myAccount.Industry = 'Technology';

// Print the account info
System.debug('Account Name: ' + myAccount.Name);
System.debug('Industry: ' + myAccount.Industry);
```

**New Concepts:**
- `Account` - Salesforce object (familiar from UI!)
- `new Account()` - Creates new record in memory (not saved to database yet)
- `myAccount.Name` - Sets the Name field (like filling out a form)

**Important:** This creates an Account in memory but doesn't save it to the database. We'll learn DML operations in Hour 2.

**✅ Executed Successfully**

---

### Example 4: Simple Math

```apex
Integer price = 100;
Integer quantity = 5;
Integer total = price * quantity;

System.debug('Price: $' + price);
System.debug('Quantity: ' + quantity);
System.debug('Total: $' + total);
```

**Math Operators:**
- `+` addition
- `-` subtraction
- `*` multiplication
- `/` division

**✅ Executed Successfully**

---

## Practice Challenges Completed

### Challenge 1: Create a Contact ✅

```apex
Contact myContact = new Contact();
myContact.FirstName = 'Jane';
myContact.LastName = 'Doe';
myContact.Email = 'jane.doe@example.com';

System.debug('Full Name: ' + myContact.FirstName + ' ' + myContact.LastName);
System.debug('Email: ' + myContact.Email);
```

**Modified Version (with Phone):**
```apex
Contact myContact = new Contact();
myContact.FirstName = 'Jane';
myContact.LastName = 'Doe';
myContact.Email = 'jane.doe@example.com';
myContact.Phone = '555-1234';

System.debug('Full Name: ' + myContact.FirstName + ' ' + myContact.LastName);
System.debug('Email: ' + myContact.Email);
System.debug('Phone: ' + myContact.Phone);
```

---

### Challenge 2: Create an Opportunity ✅

```apex
// Creating new Opportunity
Opportunity opp = new Opportunity();
opp.Name = 'Big Deal';
opp.StageName = 'Prospecting';
opp.CloseDate = Date.today();

System.debug('Opportunity: ' + opp.Name);
System.debug('Stage: ' + opp.StageName);
System.debug('Date: ' + opp.CloseDate);

```

---

### Challenge 3: Do Some Calculations ✅

```apex
Decimal revenue = 50000.00;
Decimal expenses = 30000.00;
Decimal profit = revenue - expenses;

System.debug('Revenue: $' + revenue);
System.debug('Expenses: $' + expenses);
System.debug('Profit: $' + profit);
```

**New Data Type:**
- `Decimal` - Numbers with decimal points (currency, percentages)

---

### Challenge 4: Create Multiple Variables ✅

```apex
String companyName = 'Acme Corp';
Integer numberOfEmployees = 500;
Boolean isPublic = true;
Decimal stockPrice = 125.50;

System.debug('Company: ' + companyName);
System.debug('Employees: ' + numberOfEmployees);
System.debug('Public Company: ' + isPublic);
System.debug('Stock Price: $' + stockPrice);
```

---

## Key Concepts Mastered Today

✅ How to write and execute Apex code in Developer Console  
✅ Variables and data types (String, Integer, Boolean, Decimal)  
✅ System.debug() for printing output  
✅ Creating Salesforce objects (Account, Contact, Opportunity)  
✅ Setting field values on objects  
✅ Comments with `//`  
✅ Basic math operations  
✅ String concatenation with `+`

---

## Common Beginner Mistakes to Avoid

❌ **Forgetting semicolons** - Every statement needs `;` at the end  
❌ **Misspelling field names** - `myAccount.Nmae` won't work!  
❌ **Using double quotes** - Use `'...'` not `"..."` for strings  
❌ **Case sensitivity** - `String` is correct, `string` might cause issues  

---

## Next Steps

### Immediate (Before Day 2)
1. ✅ Document today's lesson in GitHub repo
2. ⏳ Set up GitHub repo structure (week folders, README)
3. ⏳ Make first commit
4. ⏳ Review today's code examples one more time

### Tomorrow Morning (Day 1, Hour 2)
**Topic: Conditionals & DML Operations**

We'll learn:
- **If/else statements** - Making decisions in code
- **DML operations** - Actually saving records to the database (insert, update, delete)
- **First real-world scenario** - Code that does something useful

**Preparation:**
- Be ready to execute code in Developer Console
- Have GitHub repo set up for documenting Hour 2
- Come with any questions from Hour 1

---

## Personal Notes & Reflections

### What Went Well
- Executed all 4 examples successfully ✅
- Completed all 3 practice challenges ✅
- Understanding feels solid for Day 1, Hour 1 ✅
- Good decision to take a break and document ✅

### Aha Moments
- Apex objects are the same as the Salesforce objects I already know from the UI
- Code is just giving Salesforce specific instructions in a structured way
- System.debug() is like a conversation with the code - it tells me what's happening

### Questions for Later
- (Add any questions that come up during review)

---

## Progress Tracker

**Week 1 Progress:** 1/56 hours (1.8%)  
**Overall Progress:** 1/400 hours (0.25%)  
**Streak:** Day 1 ✅

**Commits Today:** 1 (this documentation)  
**Code Examples Executed:** 8  
**Challenges Completed:** 3  

---

## Motivation Check

> "You just wrote your first Apex code and crushed all the challenges on Day 1, Hour 1. Many people stare at code for days before running their first line. You dove right in. That shows you have the right mindset. Keep this momentum - you're on track to achieve your 8-week goal!"

**Tomorrow:** Hour 2 - Conditionals & DML Operations 🚀

---

**Repository:** salesforce-developer-portfolio  
**Session End Time:** February 10, 2026  
**Next Session:** February 11, 2026 (Morning)
