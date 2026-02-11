# Day 2: Conditionals & DML Operations

**Date:** February 11, 2026  
**Duration:** 2-3 hours  
**Status:** ✅ Completed  
**Prerequisites:** Day 1 (Apex Fundamentals)

---

## Table of Contents
1. [Learning Objectives](#learning-objectives)
2. [Part 1: Conditionals](#part-1-conditionals)
3. [Part 2: DML Operations](#part-2-dml-operations)
4. [Part 3: SOQL Queries](#part-3-soql-queries)
5. [Real-World Scenario](#real-world-scenario)
6. [Error Encountered & Resolution](#error-encountered--resolution)
7. [Practice Challenges](#practice-challenges)
8. [Key Takeaways](#key-takeaways)

---

## Learning Objectives

By the end of this session, you will be able to:
- ✅ Use if/else statements to make decisions in code
- ✅ INSERT records into Salesforce database
- ✅ UPDATE existing records
- ✅ DELETE records
- ✅ Query data using basic SOQL
- ✅ Work with Lists and for loops
- ✅ Debug DML errors

---

## Part 1: Conditionals

### Simple If Statement

```apex
Integer age = 25;

if (age >= 18) {
    System.debug('You are an adult');
}
```

**Key Points:**
- `if (condition)` - Code runs only if condition is true
- Use comparison operators: `>`, `<`, `>=`, `<=`, `==`, `!=`

---

### If/Else Statement

```apex
Integer temperature = 75;

if (temperature > 80) {
    System.debug('It is hot outside');
} else {
    System.debug('It is not too hot');
}
```

**Key Points:**
- `else` - Runs when condition is false
- Only ONE block executes

---

### If/Else If/Else (Multiple Conditions)

```apex
Integer score = 85;

if (score >= 90) {
    System.debug('Grade: A');
} else if (score >= 80) {
    System.debug('Grade: B');
} else if (score >= 70) {
    System.debug('Grade: C');
} else {
    System.debug('Grade: F');
}
```

**Key Points:**
- Checks conditions top-to-bottom
- Stops at FIRST true condition
- `else` catches everything else

---

### Real-World Salesforce Example

```apex
Opportunity opp = new Opportunity();
opp.Name = 'Big Deal';
opp.Amount = 150000;

if (opp.Amount > 100000) {
    System.debug('This is a HIGH VALUE opportunity!');
    opp.StageName = 'Qualification';
} else {
    System.debug('This is a standard opportunity');
    opp.StageName = 'Prospecting';
}

System.debug('Stage set to: ' + opp.StageName);
```

**Use Case:** Automatically prioritize deals based on size

---

## Part 2: DML Operations

DML = Data Manipulation Language (creating, updating, deleting records)

### INSERT - Creating Records

```apex
// Create an Account
Account acc = new Account();
acc.Name = 'Acme Corporation';
acc.Industry = 'Technology';
acc.Phone = '555-1234';

// Save to database
insert acc;

System.debug('Account created with ID: ' + acc.Id);
```

**Important:**
- `insert` saves record to database
- Salesforce assigns a unique `Id`
- Check your org - the record is actually there!

---

### INSERT Multiple Records (Bulk)

```apex
// Create a list of Contacts
List<Contact> contactsToInsert = new List<Contact>();

Contact con1 = new Contact();
con1.FirstName = 'John';
con1.LastName = 'Smith';
contactsToInsert.add(con1);

Contact con2 = new Contact();
con2.FirstName = 'Jane';
con2.LastName = 'Doe';
contactsToInsert.add(con2);

// Insert all at once (more efficient!)
insert contactsToInsert;

System.debug('Created ' + contactsToInsert.size() + ' contacts');
```

**Key Points:**
- `List<SObject>` holds multiple records
- `.add()` adds items to list
- `.size()` returns count
- Bulk operations are more efficient

---

### UPDATE - Modifying Records

```apex
// Create an Account
Account acc = new Account();
acc.Name = 'TechCorp';
acc.Industry = 'Technology';
insert acc;
System.debug('Created: ' + acc.Name + ' (ID: ' + acc.Id + ')');

// Update THE SAME record
acc.Name = 'TechCorp Industries';
acc.AnnualRevenue = 5000000;
update acc;

System.debug('Updated: ' + acc.Name);
System.debug('Revenue: $' + acc.AnnualRevenue);
```

**Important Concept:**
- Run create + update code together in ONE execution
- Same `Id` proves it's the same record
- Running separately creates TWO records (common beginner mistake!)

**To verify before/after:**
```apex
// Query and check database after each step
Account check1 = [SELECT Name, AnnualRevenue FROM Account WHERE Id = :acc.Id];
System.debug('AFTER INSERT: ' + check1.Name + ', Revenue: ' + check1.AnnualRevenue);

// ... update code ...

Account check2 = [SELECT Name, AnnualRevenue FROM Account WHERE Id = :acc.Id];
System.debug('AFTER UPDATE: ' + check2.Name + ', Revenue: ' + check2.AnnualRevenue);
```

---

### DELETE - Removing Records

```apex
// Create an Account
Account acc = new Account();
acc.Name = 'Temporary Account';
insert acc;
System.debug('Created Account with ID: ' + acc.Id);

// Delete it
delete acc;
System.debug('Account deleted!');
```

**Key Points:**
- `delete` removes record from database
- Record goes to Recycle Bin (15-day recovery)
- Use carefully in production orgs!

---

## Part 3: SOQL Queries

SOQL = Salesforce Object Query Language

### Basic Query (Single Record)

```apex
// Create test data
Account testAcc = new Account();
testAcc.Name = 'Query Test Account';
testAcc.Industry = 'Finance';
insert testAcc;

// Query for it
Account retrievedAccount = [SELECT Id, Name, Industry 
                             FROM Account 
                             WHERE Name = 'Query Test Account' 
                             LIMIT 1];

System.debug('Found Account: ' + retrievedAccount.Name);
System.debug('Industry: ' + retrievedAccount.Industry);
```

**SOQL Syntax:**
- `SELECT` - Fields to retrieve
- `FROM` - Object name
- `WHERE` - Filter condition
- `LIMIT` - Max records to return
- `[ ]` - Square brackets execute query

---

### Query Multiple Records

```apex
// Query all Technology Accounts
List<Account> techAccounts = [SELECT Id, Name, Industry 
                               FROM Account 
                               WHERE Industry = 'Technology'];

System.debug('Found ' + techAccounts.size() + ' Technology accounts');

// Loop through results
for (Account acc : techAccounts) {
    System.debug('Account: ' + acc.Name);
}
```

**Key Points:**
- Results return as `List<SObject>`
- `for` loop iterates through each record
- Syntax: `for (Type variable : collection)`

---

## Real-World Scenario

**Use Case:** Automatically update high-value opportunities

```apex
// Create test Opportunities
List<Opportunity> oppsToInsert = new List<Opportunity>();

Opportunity opp1 = new Opportunity();
opp1.Name = 'Small Deal';
opp1.Amount = 50000;
opp1.StageName = 'Prospecting';
opp1.CloseDate = Date.today().addDays(30);
oppsToInsert.add(opp1);

Opportunity opp2 = new Opportunity();
opp2.Name = 'Big Deal';
opp2.Amount = 500000;
opp2.StageName = 'Prospecting';
opp2.CloseDate = Date.today().addDays(30);
oppsToInsert.add(opp2);

insert oppsToInsert;
System.debug('Created ' + oppsToInsert.size() + ' opportunities');

// Query high-value opportunities (> $100K)
List<Opportunity> highValueOpps = [SELECT Id, Name, Amount, StageName 
                                     FROM Opportunity 
                                     WHERE Amount > 100000];

System.debug('Found ' + highValueOpps.size() + ' high-value opportunities');

// Update to Qualification stage
for (Opportunity opp : highValueOpps) {
    System.debug('Updating: ' + opp.Name + ' ($' + opp.Amount + ')');
    opp.StageName = 'Qualification';
}

update highValueOpps;

System.debug('✅ Updated ' + highValueOpps.size() + ' opportunities');
```

**This demonstrates:**
1. Bulk INSERT
2. SOQL query with filter
3. Conditional logic
4. Bulk UPDATE
5. Production-ready automation pattern

---

## Error Encountered & Resolution

### The Problem

**Error Message:**
```
Line: 29, Column: 1
System.DmlException: Update failed. First exception on row 9 with id 003g5000002Dp5OAAS; 
first error: INVALID_EMAIL_ADDRESS, Email: invalid email address: b.levy@expressl&t.net: [Email]
```

**What Happened:**
- Query returned ALL contacts with emails (including old test data)
- One old contact had invalid email with `&` character
- DML update failed validation
- Salesforce enforces email format rules

---

### Root Cause

```apex
// This query was TOO BROAD
List<Contact> contactsWithEmail = [SELECT Id, FirstName, LastName, Email 
                                    FROM Contact 
                                    WHERE Email != null];
```

**Problem:** Grabbed all contacts in org, including old FilmClub data with bad emails

---

### Solution 1: Filter Query to Only New Records (BEST)

```apex
// Create new contacts
Contact c1 = new Contact();
c1.FirstName = 'John';
c1.LastName = 'Smith';
c1.Email = 'john@example.com';

Contact c2 = new Contact();
c2.FirstName = 'Jane';
c2.LastName = 'Doe';

Contact c3 = new Contact();
c3.FirstName = 'Bob';
c3.LastName = 'Johnson';
c3.Email = 'bob@example.com';

List<Contact> contacts = new List<Contact>{c1, c2, c3};
insert contacts;

// Collect IDs of contacts we just created
Set<Id> newContactIds = new Set<Id>();
for (Contact con : contacts) {
    newContactIds.add(con.Id);
}

// Query ONLY our new contacts
List<Contact> contactsWithEmail = [SELECT Id, FirstName, LastName, Email 
                                    FROM Contact 
                                    WHERE Id IN :newContactIds
                                    AND Email != null];

// Now update safely
for (Contact con : contactsWithEmail) {
    con.Description = 'Has Email Address';
}

update contactsWithEmail;
System.debug('✅ Updated ' + contactsWithEmail.size() + ' contacts');
```

**Why this works:**
- `WHERE Id IN :newContactIds` - Only touches records we created
- Avoids old test data with validation issues
- Safe and precise

---

### Solution 2: Clean Up Old Test Data

```apex
// Delete old contacts from previous testing
List<Contact> oldContacts = [SELECT Id FROM Contact WHERE CreatedDate < TODAY];
delete oldContacts;

System.debug('✅ Deleted ' + oldContacts.size() + ' old test contacts');
```

**Benefits:**
- Clean slate for learning
- No conflicts with old data
- Records go to Recycle Bin (recoverable)

---

### Solution 3: Fix the Bad Data

```apex
// Query contacts with invalid email
List<Contact> badEmailContacts = [SELECT Id, Email 
                                   FROM Contact 
                                   WHERE Email LIKE '%&%'];

// Fix the email
for (Contact con : badEmailContacts) {
    con.Email = con.Email.replace('&', 'and');
}

update badEmailContacts;
```

**Use case:** Data cleanup in real orgs

---

### Key Lessons Learned

1. **Always filter queries carefully** - Don't accidentally touch records you don't own
2. **DML can fail** - Salesforce validates data (email format, required fields, etc.)
3. **Error messages are helpful** - They tell you exactly what's wrong and where
4. **Old test data causes issues** - Clean up or filter it out
5. **Use `WHERE Id IN :setOfIds`** - Precise filtering prevents accidents

---

## Practice Challenges

### Challenge 1: Contact Email Filter (Revised)

Create 3 Contacts. Query and update only those with email addresses.

```apex
// Create contacts
Contact c1 = new Contact();
c1.FirstName = 'John';
c1.LastName = 'Smith';
c1.Email = 'john@example.com';

Contact c2 = new Contact();
c2.FirstName = 'Jane';
c2.LastName = 'Doe';
// No email

Contact c3 = new Contact();
c3.FirstName = 'Bob';
c3.LastName = 'Johnson';
c3.Email = 'bob@example.com';

List<Contact> contacts = new List<Contact>{c1, c2, c3};
insert contacts;

// YOUR CODE: Query only contacts with emails and update them
```

---

### Challenge 2: Account Revenue Categorization

Create 5 Accounts with different revenues. Categorize as Small/Medium/Large.

```apex
// Create accounts
List<Account> accounts = new List<Account>();

Account a1 = new Account(Name = 'Small Business', AnnualRevenue = 500000);
Account a2 = new Account(Name = 'Medium Business', AnnualRevenue = 5000000);
Account a3 = new Account(Name = 'Large Enterprise', AnnualRevenue = 50000000);

accounts.add(a1);
accounts.add(a2);
accounts.add(a3);

insert accounts;

// YOUR CODE: Query, categorize, and update Type field
// Small: < $1M
// Medium: $1M - $10M  
// Large: > $10M
```

---

### Challenge 3: Opportunity Cleanup

Create 3 Opportunities. Delete any with Amount < $10,000.

```apex
// YOUR CODE: Create opportunities with different amounts
// Query low-value opportunities
// Delete them
```

---

## Key Takeaways

### Technical Skills Acquired
✅ **Conditionals** - if/else for business logic  
✅ **DML Operations** - INSERT, UPDATE, DELETE  
✅ **SOQL Queries** - SELECT, FROM, WHERE, LIMIT  
✅ **Collections** - List, Set basics  
✅ **Loops** - for loop iteration  
✅ **Error Handling** - Reading and resolving DML exceptions  

### Developer Mindset
✅ **Always filter queries** - Be precise, avoid accidents  
✅ **Read error messages carefully** - They guide you to solutions  
✅ **Test with clean data** - Old data causes unexpected issues  
✅ **Think about validation** - Salesforce enforces rules  
✅ **Use System.debug strategically** - Track what's happening  

### Interview-Ready Knowledge

**Q: "Write code to query and update records"**
```apex
List<Account> accounts = [SELECT Id, Name FROM Account WHERE Industry = 'Technology'];
for (Account acc : accounts) {
    acc.Rating = 'Hot';
}
update accounts;
```

**Q: "How do you handle DML errors?"**
- Read error message to identify issue
- Filter queries to avoid problematic records
- Use try-catch for graceful error handling (learned later)
- Validate data before DML operations

**Q: "What's the difference between creating a record in memory vs database?"**
- `new Account()` - Creates in memory only
- `insert acc` - Saves to database, assigns Id
- Memory records lost after execution; database records persist

---

## Progress Tracker

**Day 2 Complete** ✅

**Concepts Mastered:**
- Conditionals (if/else/else if)
- DML (INSERT, UPDATE, DELETE)
- SOQL (SELECT, WHERE, LIMIT)
- Lists and for loops
- Error debugging

**Code Examples Executed:** 10+  
**Challenges Completed:** 3  
**Errors Debugged:** 1 (Invalid email format)  
**Real Records Created:** Multiple Accounts, Contacts, Opportunities  

**Next Session:** Day 2 - Collections (List, Set, Map) & Advanced Loops

---

## Additional Resources

**Official Salesforce Documentation:**
- [Apex Developer Guide - DML Operations](https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_dml.htm)
- [SOQL and SOSL Reference](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/)

**Trailhead Modules:**
- Apex Basics & Database
- SOQL for Admins

---

**Status:** Ready for Day 3 🚀  
**Confidence Level:** High  
**Momentum:** Strong  

---

*Document created: February 11, 2026*  
*Part of: [Salesforce Developer Portfolio](https://github.com/yourusername/salesforce-developer-portfolio)*
