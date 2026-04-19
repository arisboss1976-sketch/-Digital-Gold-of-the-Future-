### 1. `index.html`
```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>VaultNote</title>
    <link rel="stylesheet" href="/src/styles.css" />
</head>

<body>
    <div id="app"></div>
    <script type="module" src="/src/main.js"></script>
</body>

</html>
```

### 2. `styles.css`
```css
:root {
    --bg-color: rgba(11, 18, 32, 0.9);
    --panel-color: rgba(17, 26, 46, 0.85);
    --text-color: #e7eefc;
    --muted-color: #a9b7d6;
    --brand-color: #6ea8fe;
    --success-color: #44d19d;
    --warning-color: #ffcc66;
    --error-color: #ff6b6b;
    --border-color: rgba(255, 255, 255, 0.1);
    --shadow-color: rgba(0, 0, 0, 0.3);
    --border-radius: 12px;
}

* {
    box-sizing: border-box;
}

html, body {
    height: 100%;
    margin: 0;
    font-family: 'Arial', sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    background: url('src/background.jpg') no-repeat center center fixed;
    background-size: cover;
    color: var(--text-color);
}

#app {
    width: 100%;
    max-width: 1200px;
    padding: 20px;
}

.container {
    background: var(--panel-color);
    border-radius: var(--border-radius);
    box-shadow: 0 4px 20px var(--shadow-color);
    padding: 40px;
    animation: fadeIn 1s ease-in-out;
}

h1 {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 20px;
    color: var(--brand-color);
}

/* Card Styles */
.card {
    background: linear-gradient(180deg, rgba(255, 255, 255, 0.05), transparent), var(--panel-color);
    border: 1px solid var(--border-color);
    border-radius: var(--border-radius);
    box-shadow: 0 2px 10px var(--shadow-color);
    padding: 20px;
    margin: 20px 0;
    transition: transform 0.3s;
}

.card:hover {
    transform: translateY(-5px);
}

.card-title {
    font-size: 1.5rem;
    margin-bottom: 10px;
    color: var(--success-color);
}

.card-content {
    font-size: 1rem;
    color: var(--muted-color);
}

.grid {
    display: flex;
    flex-direction: column;
    gap: 20px;
}
@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}
```

### 3. `main.js`
```javascript
import "./styles.css";

const API = ""; // API endpoint (ถ้ามี)

let csrfToken = null;
let me = null;
let records = [];
let decryptedCache = new Map();

function h(tag, attrs = {}, ...children) {
    const e = document.createElement(tag);
    for (const [k, v] of Object.entries(attrs || {})) {
        if (k === "on") for (const [ev, fn] of Object.entries(v)) e.addEventListener(ev, fn);
        else e.setAttribute(k, v);
    }
    for (const c of children.flat()) e.append(c?.nodeType ? c : document.createTextNode(String(c)));
    return e;
}

// API call handler (simplified)
async function api(path, { method = "GET", body } = {}) {
    // การดำเนินการ API
}

// กิ่งฟังก์ชันอื่น ๆ
async function loadMe() {
    // โหลดข้อมูลผู้ใช้
}

async function loadRecords() {
    // โหลดบันทึก
}

async function app() {
    const root = document.querySelector("#app");
    root.innerHTML = "";

    // สร้าง UI
    const header = h("h1", {}, "Welcome to VaultNote");
    const authCard = h("div", { class: "card" }, 
        h("h2", { class: "card-title" }, "Authentication"),
        h("div", { class: "card-content" }, "Authenticate users securely.")
    );
    const vaultCard = h("div", { class: "card" }, 
        h("h2", { class: "card-title" }, "Vault"),
        h("div", { class: "card-content" }, "Manage your encrypted notes.")
    );
    const recordsCard = h("div", { class: "card" }, 
        h("h2", { class: "card-title" }, "Records Management"),
        h("div", { class: "card-content" }, "View and manage your stored records.")
    );

    root.append(
        h("div", { class: "container" },
            header,
            h("div", { class: "grid" },
                authCard,
                vaultCard
            ),
            recordsCard
        )
    );

    // โหลดข้อมูลโดยเริ่มต้น
    (async () => {
        await loadMe(); // โหลดผู้ใช้
        await loadRecords(); // โหลดบันทึก
    })();
}

app();
```
