### 🐞 1 Program, 4 Business Logic Bugs and Cashing in 2300$.
- Type: Writeup  
- Author:  Manav Bankatwala

---

### First Bug

### 🔍 Summarys
- Business Logic in inviting additional members
As mentioned, that in a Team plan, we can only invite up to 3 members and then per member addition cost was 32$.
The bugs here is that when we send an invitaion link to add members to our team is that if we have three members in the team it will show that we reach our limit as it suppose to work.
However, if we clear our members to become 0 and send invitation links to the amount of people we want then ask them to use the link latter after sent them, we can have bypass the 3 limit by that.

### 🧠 Root Cause
- The root cause of the problem is that the system does start count members  until when the invitee use the link or the system check the number of members in a team before the user is being added and apply charges.

---

### ⚙️ Exploitation Steps

1. Enter the details of member and send the invitation link.
2. Don’t use the link and again add another member.
3. Repeat the process till the number of users you want to add.
4. Still the member count is 0 in plan as no one has accepted the invitation yet.
5. Now, visit all the invitation links sent one by one. All the members will be added without any charges. Like this I invited more than 6 users and saved 200$.


---

### 💡 Key Learning
-  Send the link more than the allow number of members and then use them the system may act wied as in this case.

---

### Second Bug: No Plan user can invite members

---

### 🔍 Summarys
- No Plan user can invite members
Again here, a user with no plan cannot access the feature of inviting other members into the team. But due to the presence of a security misconfiguration, 
we can directly send the API call of invite user with no plan user session token.

### 🧠 Root Cause
- Here cause of the problem is that the system hide the button for invite in the UI. However, the backend does not check whether user is allow to invite or not.

---

### ⚙️ Exploitation Steps

1. Capture the POST request responsible for inviting new user and send this request to repeater.
2. Change the authorization token to a user token having no plan. Also changed the workspace ID parameter.
3. Sent the request and it was successful. Instead of showing a forbidden error. The user was invited.


---

### 💡 Key Learning
-  The key learning is that don't trust front if the frontend say is not allow take the endpoint and grab your burpsuite.

---

### Third Vulnerability : Race condition in creating browser profiles
---

### 🔍 Summarys
-Here, in the application we are only assigned a specific number of browser profiles to create. 
For example, we can only create 300 browser profiles with a solo plan. This looked like a case for me to test 
for race condition i.e. if we can create more than 300 profiles with a limited plan access.


### 🧠 Root Cause
- The system failed to process multiple request at once correctly which lead to bypass the 300 limit.
---

### ⚙️ Exploitation Steps

 I first created 298 profiles

1. Then again clicked on create a new profile and capture the request in burp suite.

2. Sent this request to extension, Turbo Intruder. You can even use your own python script. Added a random position as payload position and increased the threads.

3. As the attack ended. The total count of browser profiles was 306. This indicated a successful exploit of race condition. Easy right?

---

### 💡 Key Learning
-  Race condition can be used to bypass limit. 

---

- source link: https://infosecwriteups.com/1-program-4-business-logic-bugs-and-cashing-in-2300-299b42236993 
