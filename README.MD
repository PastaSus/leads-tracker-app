Here’s a **README.md** for your Leads Tracker app, explaining what it does, how it works, and what lessons can be learned from the code.

---

## 🚀 Leads Tracker

A simple web app that tracks and saves leads (URLs) using Firebase as a Backend-as-a-Service (BaaS). The app allows users to input links, store them in Firebase Realtime Database, and retrieve them dynamically.

### 📌 Features

✅ Add and save leads (URLs) to Firebase  
✅ Display saved leads dynamically on the page  
✅ Delete all leads with a double-click  
✅ Uses Firebase Realtime Database for seamless data syncing

### 🛠️ Technologies Used

- **JavaScript** – Frontend logic and event handling
- **Firebase Realtime Database** – Cloud-based data storage
- **HTML & CSS** – Basic UI structure
- **ES Modules** – Imports Firebase SDK from CDN

### 🔥 Lessons from the Code

#### 1️⃣ **Initializing Firebase in JavaScript**

```js
const firebaseConfig = {
  databaseURL:
    "https://leads-tracker-app-6e18d-default-rtdb.asia-southeast1.firebasedatabase.app",
};
const app = initializeApp(firebaseConfig);
const database = getDatabase(app);
const referenceInDB = ref(database, "leads");
```

**What it does:**

- Connects the app to Firebase using the `firebaseConfig`.
- Gets a reference (`ref()`) to the `"leads"` section in the database.

---

#### 2️⃣ **Adding Data to Firebase**

```js
inputBtn.addEventListener("click", function () {
  push(referenceInDB, inputEl.value);
  inputEl.value = "";
});
```

**What it does:**

- Listens for button clicks and adds input values to Firebase using `push()`.

---

#### 3️⃣ **Fetching Data from Firebase**

```js
onValue(referenceInDB, function (snapshot) {
  const snapshotDoesExist = snapshot.exists();
  if (snapshotDoesExist) {
    const snapshotValues = snapshot.val();
    const leads = Object.values(snapshotValues);
    render(leads);
  }
});
```

**What it does:**

- `onValue()` listens for database changes and updates the UI dynamically.
- `snapshot.exists()` checks if data exists before trying to retrieve it.

---

#### 4️⃣ **Displaying Data in the UI**

```js
function render(leads) {
  let listItems = "";
  for (let i = 0; i < leads.length; i++) {
    listItems += `
      <li>
        <a target='_blank' href='${leads[i]}'>${leads[i]}</a>
      </li>
    `;
  }
  ulEl.innerHTML = listItems;
}
```

**What it does:**

- Loops through the leads and dynamically updates the list (`ulEl`).

---

#### 5️⃣ **Deleting All Leads**

```js
deleteBtn.addEventListener("dblclick", function () {
  remove(referenceInDB);
  ulEl.innerHTML = "";
});
```

**What it does:**

- Listens for a **double-click** event and deletes all stored leads using `remove()`.

---

### 📜 Author

Developed by **Aaron Cerezo**
