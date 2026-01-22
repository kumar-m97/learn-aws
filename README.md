# Learn AWS

**##Random Topics are covered##**

## ACL Configuration:  
In AWS Network ACLs (NACLs), rule numbers control evaluation order. Lower numbers are evaluated first.  

### ✅ How rules 100 and 200 work  
AWS evaluates rule 100 first  
If rule 100 matches, AWS applies the action immediately (ALLOW or DENY)  
Rule 200 is ignored if rule 100 already matched  
If rule 100 does NOT match, AWS moves to rule 200  
👉 First match wins. No further rules are checked.  

### Example  
<img width="906" height="271" alt="image" src="https://github.com/user-attachments/assets/3582f268-2993-4ea4-95a0-537c79371b7e" />  

**What happens?**
SSH traffic from 10.0.5.10  
Matches rule 100  
✅ ALLOWED  
Rule 200 never evaluated  

HTTP traffic from 10.0.5.10  
Does not match rule 100  
Matches rule 200  
❌ DENIED  

<img width="1040" height="329" alt="image" src="https://github.com/user-attachments/assets/69c1c3f2-cc15-4964-96d6-b73a4034774d" />


