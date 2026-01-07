## Deadlines

- Hand in HLD: 19/11/25

## Tasks

### Tasks until 12/11/25

- ~~Achieve a good draft of the HLD.~~
- Making sure that everyone have read the draft, and took part.
- ~~Asking feedback for fixes before handing in.~~
- [x]  User stories-**Inbar**
- [x]  use case diagram **-Sagie**
- [x]  sequence diagram-**Inbar**
- [x]  break down into tasks, and then into issues+task acceptance critiria-**Itamar**
- [x]  Alternatives & disccusion-**Inbar**
- [x]  Deployment diagram - **Yonatan**
- [x]  CI/CD plan-**Inbar**
- [x]  Risk managment-**Inbar**

### Tasks until 19/11/25

- ~~Get feedback on HLD, and improve.~~
- Make sure that everyone have seen the HLD, went over, and verified that it is OK.
- ~~Hand in HLD~~
- ~~Open a platfrom in github for the project.~~
- Make sure that everyone have a way to run and check flutter.
- ~~Design first sprint (goals,work management…)~~
- ~~Have a deadline for first sprint (MVP ASAP)~~
    
    

### Tasks for 3/12/25

- Combine the current project to a coherent one.
    - combine the flutter fromtend parts to interact with each other
    - Make sure that the fromtend can interact with the bacend using the interLayer
- Make sure that the design is as expected from HAMAL (i.e similar to the HAMAL website)
- Ask if there is a decision about the CRM/xRM. What can we modify, what tools…

# Weekly summeries

### 5/11/25-Itamar

Today we discussed the core values our platform needs to provide to volunteers — primarily the ability to receive push notifications for new tasks along with clear task descriptions. We defined our MVP scope, focusing on enabling two-way communication: after user login, volunteers will complete a short onboarding questionnaire and then be able get to receive tasks and also mark them with labels such as DONE/PENDING as a way to communicate(like in Jira).
The application should be cross-platform and will collect user location data and preferences for task suggestions. We also noted the need to test push notifications through the web application.
Additionally, we reviewed the project structure and we were told that the HDL must be submitted within 2 weeks from now. Every group member must contribute his share in the creation of the HLD and review it.
We also need to cooperate with the other team working on the Delivery Management project so the technologies that the two groups will use are going to be similar.

19/11/25 - Yonatan

---

# **Project Architecture & Meeting Summary — 19.11**

## **Goal**

Build a Flutter application (Android + iOS) that integrates with an external xRM system which manages volunteering events and volunteers.

Since the client’s xRM is not yet known, we will build the system around a **mock xRM environment** and clean interfaces, allowing easy integration later.

---

# **📌 Meeting Summary (19.11)**

### **1. Create a Mock xRM Environment**

- We will build a **simulated xRM backend**, using something simple like **SQLite** or any lightweight DB.
- This mock xRM will provide:
    - Fake events
    - Fake volunteer data
    - Fake approval workflows
- Purpose:
    - Full end-to-end development and testing **without touching the client’s real database**.
    - A “sterile environment” that we fully control.

### **2. Only integrate with the real xRM when the product is complete**

- The final app must be tested from all angles using our mock system.
- Only after the app is fully stable, we will create the integration adapter to the real xRM.
- We will *not* connect to the client's database during development.

### **3. Admin Approval Workflow (Optional Future Feature)**

- At the end, instead of writing directly into the xRM database:
    - Our backend may send “event status cards” or “new volunteer entries”
    - A client admin approves them manually
    - Only then data is inserted into their system
        
        *(This avoids permissions issues and keeps the xRM safe.)*
        

### **4. Platforms**

- **Focus first on Android** (easier to test).
- Later, build an **iOS Unlisted Release** for testing:
    
    https://developer.apple.com/support/unlisted-app-distribution/
    

### **5. Backend & Database**

- Backend will be written in **Python** (FastAPI / Flask / Django).
- Database may be hosted on **Azure**; need to check pricing.
- Flutter will communicate with this backend only.

### **6. Authentication**

- Authentication: **Firebase Auth** (Google Sign-In etc.)
- All other data (tasks, filters, events, volunteers): stored in **our backend + database**, not in Firebase. (actually maybe not? this can also be on firebase. we don’t care yet. )

### **7. Flutter Architecture**

Flutter will expose a **very clean, generic interface (Repository pattern)**.

The Flutter app will not depend on:

- Which backend exists
- Which database exists
- Which xRM is used

This makes the system maintainable and easy to swap components later.

---

# **🖼️ System Architecture**

```
Flutter UI
   ↓
EventRepository / UserRepository (Flutter)
   ↓
RestEventRepository / RestUserRepository (Flutter)
   ↓  (HTTP GET/POST)
Python Server (FastAPI / Flask / Django)
   ↓
Mock Database (MongoDB) → Later: Real xRM Integration Layer

```

---

# **🧩 Flutter Request/Response Interface (API Layer)**

These are the abstract interfaces Flutter will call.

The backend (mock xRM now, real xRM later) will implement them.

---

## **🔐 User Information Interface**

### **GetUserIdByName(name) → string**

Returns the internal user ID.

### **GetUserFiltersById(id) → Filter[]**

Returns all saved filters of a user.

### **AddFilterToUser(filter, id) → None**

Adds a new filter for the user.

### **AddNewUser(id, filters[]) → None**

Creates a new user.

`filters` may be empty or pre-populated.

---

## **📅 Event Information Interface**

### **GetEventsByFilters(filters[]) → Event[]**

Returns all event objects that match the given filters.

### **UpdateEventStatus(event) → None**

(Not for now, but part of final integration)

Sends updated event status back to the xRM/server:

- number of volunteers signed up
- volunteer IDs
- event completion info
- etc

---

# Sprints

## Sprint 1

in charge of progress-**Inbar**

- [x]  Regsiter Mechanism with google - **Yonatan**
- [x]  SIgn in Mechanism with google - **Yonatan**
- [x]  change preferences page-**Itamar**
- [x]  backend Python DB-**Inbar**
- [x]  create the interface on dart-**Roman** (please check with Inbar on syntax of messages)
    - the methods on meeting 19.11
- [x]  events page-**Sagie**
    - Able to filter (by default) by  user prefrences.
    - Search by any prefrences.
    - Sign in to an activity.
    - Un sign from an activity.
- [x]  Helper (check if any need help)-**Andrii**

## Sprint 2

The polish and pages sprint? (maybe)

- [x]  Change user id to string in Backend-**Inbar**
- [x]  Change user id to string in interlayer-**Roman**
- [x]  Finish integration of filters add/remove-**Itamar**
- [x]  Finish integration of personalize filters-**Sagie**
- [x]  Add a settings page (mostly for location usage)- **Andrii**
- [x]  Add a search page for activities near you (by location from app, and date)- **Yonathan**
- [ ]  Add a view my activities page to check your activities (same as normal, just what I signed for)- **Sagie**
- [x]  Add a news page to view news- **Itamar**
- [x]  Add the new elemets in the interlayer- **Roman**
- [x]  Add a backend use for news-**Inbar**
- [x]  Add a backend for getting activities by location-**Inbar**
- [x]  Add an option to get activities in bulks (page,page size)-**Inbar**
- [x]  Add get my signed activities-**Inbar**

## Sprint 2.67

- [ ]  Update the filter by your filters (last sprint remain)-**Sagie**
- [ ]  Update news fetching by date (last sprint remains)-**Itamar**
- [ ]  Update that each time you enter the choose filters window you fetch the filters (last sprint remains)-**Itamar**
- [ ]  Add a view my activities page to check your activities (same as normal, just what I signed for) (last sprint remains)-**Sagie**

## Sprint 3

- [x]  Change the location matcher.-**Inbar**
- [ ]  English-Hebrew transformation.-**Itamar+Andrii**
- [x]  Supporte phones in firebase.-**Yonathan**
- [x]  Users have points! (gonna be fun). backend-**Inbar**
- [ ]  Users have points! (gonna be fun). interlayer-**Roman**
- [ ]  Understand how to use zoho.-**Inbar**
- [ ]  sign Up-**Sagie**
- [x]  Sign up backend-**Inbar**
- [ ]  Play store stuff-**Yonathan**


סיכום דרישות מהלקוח:

1. עדיף תמיכה בעברית אנגלית, אם לא אז רק עברית.
2. לשנות מיקום לרמת האזור
3. התממשקות עם xRM כל שינוי אצלנו משתקף ב-xRM ולהיפך 
4. לא צריך אדמין, הכל דרך ה-xRM
5. מזהה הוא מספר טלפון (לא רק ישראלי)
6. לא צריך לטפל בביטוח, זה אצלם.
7. יש שירות וואטספ/הודעת sms (זו כנראה תהיה האותנטיקציה)
8. רשימת תפוצה (להעביר ל-xRM)
9. לכל משתמש שם,טלפון,אימייל,אזור מגורים.
10. מידע רגיש-ת”ז,פציעות,גיל(כטווח)
11. כישורים (אפילו כפילטר)
12. לדעת מה ההתנדבות של כל אחד
13. אם לא מילא ביטוח לאומי, צריך למלא הצהרה.
14. מסך הרשמה ראשונה של ביטוח לאומי+העדפות+כישורים

היי, נשמח לוודא מספר דברים:

1. בנושא ה-xRM., האם הציפייה היא שבאפליקציה הסופית אנחנו נתממשק אך ורק מולו? ואולי יהיה עוד מסד נתונים קטן לשמירת נתונים (למשל העדפות של מתנדב, או פילטרים של אירוע). האם המטרה שאותם פילטרים יישמרו רק ב-xRM בסוף? למשל האם זה אירוע שדורש הנדימן, או המיקום (ברמת תת אזור/אזור)? כלומר אנחנו מנסים להבין האם יש בכלל צורך מבחינתכם במסד נתונים נוסף לאפליקציה, או שעדיף להשתמש אך ורק ב-xRM?
2. האם הרישום הוא אצלכם? כלומר באפליקציה מתחברים דרך מספר טלפון שאמור להיות קיים כבר ב-xRM?
3. האם ניתן להוסיף לאופן שבו אתם שומרים משתמשים מידע נוסף? למשל הזכרתם שייתכן ולאחר כל התנדבות יקבלו המתנדבים נקודות (שלאחר מכן ישמשו לשוברי קנייה). אז האם ניתן להניח שזה שדה ב-xRM?
