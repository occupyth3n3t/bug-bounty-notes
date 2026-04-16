### 🐞 Accessing deleted comment for $$: A Bug Bounty Writeup
- Type: Writeup  
- Author:  the_unlucky_guy

---

### 🔍 Summarys
- After exploring the website, I started reviewing all the requests and responses from the community.redacted.com. 
There is one GET endpoint https://community.redacted.com/ajax/ugc/frontend/comment/getComment?id=comment_id&tid=thread_id
which is used to fetch comment from the thread based on the parameter id=comment_id&tid=thread_id . Both comment_id and thread_id 
is long numeric string. I open the GET endpoint https://community.redacted.com/ajax/ugc/frontend/comment/getComment?id=comment_id&tid=thread_id 
in the browser and found that all the comment from my thread is visible in the JSON response.

### 🧠 Root Cause
- The root cause of the vulrabilities is that the system does not delete the commend from the database/server.

---

### ⚙️ Exploitation Steps

1. Delete the comment from your threads using the delete button in UI.
2. Reopen this endpoint https://community.redacted.com/ajax/ugc/frontend/comment/getComment?id=comment_id&tid=thread_id in the browser and found that the deleted comment is still visible in JSON response. 
Thread comment is only deleted from the UI but not actually deleted from the backend/database so anyone or thread owner can access the deleted comment of the thread.

---

### 💡 Key Learning
-  Even when UI is not showing it, visit the json endpoint it may be still available.

---

source link: https://vijetareigns.medium.com/accessing-deleted-comment-for-a-bug-bounty-writeup-95d56662d209

---
