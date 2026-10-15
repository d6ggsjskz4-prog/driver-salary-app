# driver-salary-app
Driver salary calculator
<!DOCTYPE html>
<html lang="uk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#101827">
<title>Мої рейси — зарплата водія</title>

<style>
:root {
  --bg: #101827;
  --card: #192438;
  --field: #101a2b;
  --text: #f2f5fb;
  --muted: #9aa9bf;
  --accent: #56d6a0;
  --blue: #6ea8ff;
  --danger: #ff7373;
  --border: #2b3b53;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  padding: 16px;
  background: var(--bg);
  color: var(--text);
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}
main { max-width: 760px; margin: auto; }
header { padding: 8px 2px 18px; }
h1 { font-size: 27px; margin: 0 0 7px; }
h2 { font-size: 18px; margin: 0 0 16px; }
h3 { font-size: 15px; margin: 0 0 10px; }
p { line-height: 1.5; }
.small { color: var(--muted); font-size: 12px; }
.card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 18px;
  padding: 17px;
  margin-bottom: 15px;
}
.stats {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 10px;
}
.stat {
  min-width: 0;
  background: var(--field);
  padding: 13px;
  border-radius: 13px;
  border: 1px solid var(--border);
}
.stat strong {
  display: block;
  color: var(--accent);
  font-size: 20px;
  overflow-wrap: anywhere;
  margin: 7px 0;
}
.statline { margin-top: 5px; font-size: 13px; color: var(--muted); }
label {
  display: block;
  font-size: 13px;
  color: var(--muted);
  margin: 0 0 6px;
}
input, select, textarea {
  width: 100%;
  background: var(--field);
  border: 1px solid var(--border);
  color: var(--text);
  padding: 12px;
  border-radius: 10px;
  font: inherit;
  font-size: 15px;
  outline: none;
}
input:focus, select:focus, textarea:focus {
  border-color: var(--blue);
}
textarea { min-height: 75px; resize: vertical; }
.field { margin-bottom: 13px; min-width: 0; }
.grid2 {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 12px;
}
button {
  border: 0;
  border-radius: 11px;
  padding: 12px 14px;
  background: var(--accent);
  color: #092319;
  font-size: 14px;
  font-weight: 700;
  cursor: pointer;
}
button.secondary {
  background: #2a3b55;
  color: var(--text);
}
button.danger {
  background: #492b37;
  color: #ffb1b1;
}
button:active { opacity: .8; }
.buttons {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-top: 12px;
}
.buttons button { flex: 1; }
.sectionline {
  border-top: 1px solid var(--border);
  margin: 18px 0;
}
.linebox {
  background: var(--field);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 11px;
  margin-bottom: 9px;
}
.linebox .grid2 { gap: 8px; }
.linebox input, .linebox select { padding: 10px; }
.lineitem {
  padding: 9px 0;
  border-bottom: 1px solid var(--border);
  font-size: 13px;
  overflow-wrap: anywhere;
}
.lineitem:last-child { border-bottom: 0; }
.lineitem button {
  padding: 5px 9px;
  float: right;
  font-size: 12px;
}
.trip {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 15px;
  margin-bottom: 12px;
}
.triptop {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 10px;
}
.triproute {
  font-size: 17px;
  font-weight: 750;
  overflow-wrap: anywhere;
}
.tripmeta {
  color: var(--muted);
  font-size: 12px;
  line-height: 1.6;
  margin-top: 5px;
  overflow-wrap: anywhere;
}
.pill {
  background: #263851;
  border-radius: 20px;
  padding: 5px 9px;
  font-size: 12px;
  flex-shrink: 0;
}
.tripbalance {
  color: var(--accent);
  font-size: 25px;
  font-weight: 800;
  margin-top: 15px;
  overflow-wrap: anywhere;
}
.tripdetails {
  margin-top: 12px;
  padding-top: 9px;
  border-top: 1px solid var(--border);
  font-size: 13px;
  line-height: 1.7;
  overflow-wrap: anywhere;
}
.empty {
  text-align: center;
  color: var(--muted);
  padding: 25px 12px;
}
.notice {
  background: #20374a;
  color: #d5e8ff;
  border-radius: 10px;
  padding: 10px;
  font-size: 12px;
  line-height: 1.5;
  margin-top: 12px;
}
#status {
  font-size: 12px;
  color: var(--muted);
  margin: 8px 2px;
}
@media (max-width: 420px) {
  body { padding: 10px; }
  .card { padding: 13px; }
  .stat { padding: 10px; }
  .stat strong { font-size: 17px; }
  .grid2 { gap: 8px; }
}
</style>
</head>

<body>
<main>
  <header>
    <h1>🚛 Мої рейси</h1>
    <div class="small">Облік рейсів, зарплати, авансів і видатків</div>
  </header>

  <!-- ЗАГАЛЬНА СТАТИСТИКА -->
  <section class="card">
    <h2>📊 Загальна статистика</h2>
    <div class="stats">
      <div class="stat">
        <span class="small">Зарплата · EUR</span>
        <strong id="totalSalaryEUR">0,00 €</strong>
        <div class="statline">Аванси: <span id="totalAdvEUR">0,00 €</span></div>
        <div class="statline">Видатки: <span id="totalExpEUR">0,00 €</span></div>
      </div>
      <div class="stat">
        <span class="small">Зарплата · UAH</span>
        <strong id="totalSalaryUAH">0,00 ₴</strong>
        <div class="statline">Аванси: <span id="totalAdvUAH">0,00 ₴</span></div>
        <div class="statline">Видатки: <span id="totalExpUAH">0,00 ₴</span></div>
      </div>
    </div>
    <p class="small">загальна сума</p>
  </section>

  <!-- ФОРМА РЕЙСУ -->
  <section class="card">
    <h2 id="formTitle">➕ Додати рейс</h2>

    <form id="tripForm">
      <input type="hidden" id="editId">

      <div class="field">
        <label for="tripDate">Дата рейсу</label>
        <input type="date" id="tripDate" required>
      </div>

      <div class="field">
        <label for="route">Маршрут</label>
        <input id="route" placeholder="Наприклад: Італія — Україна" required>
      </div>

      <div class="grid2">
        <div class="field">
          <label for="freight">Сума фрахту</label>
          <input type="number" id="freight" min="0" step="0.01" placeholder="2500" required>
        </div>
        <div class="field">
          <label for="currency">Валюта фрахту</label>
          <select id="currency">
            <option value="EUR">Євро (€)</option>
            <option value="UAH">Гривня (₴)</option>
          </select>
        </div>
      </div>

      <div class="grid2">
        <div class="field">
          <label for="percent">Зарплата (%)</label>
          <input type="number" id="percent" min="0" max="100" step="0.1" value="17" required>
        </div>
        <div class="field">
          <label for="tripRate">Курс EUR → UAH</label>
          <input type="number" id="tripRate" min="0" step="0.0001" placeholder="Наприклад: 48.50" required>
        </div>
      </div>

      <div class="notice">
        Курс зберігається окремо для кожного рейсу. Для наступного рейсу автоматично підставиться останній використаний курс.
      </div>

      <div class="sectionline"></div>

      <h3>💶 Аванси</h3>
      <div class="linebox">
        <div class="field">
          <label for="advNote">За що виданий аванс</label>
          <input id="advNote" placeholder="Наприклад: аванс від фірми">
        </div>
        <div class="grid2">
          <div class="field">
            <label for="advAmount">Сума</label>
            <input id="advAmount" type="number" min="0" step="0.01" placeholder="100">
          </div>
          <div class="field">
            <label for="advCurrency">Валюта</label>
            <select id="advCurrency">
              <option value="EUR">Євро (€)</option>
              <option value="UAH">Гривня (₴)</option>
            </select>
          </div>
        </div>
        <button type="button" class="secondary" id="addAdvance">+ Додати аванс</button>
      </div>
      <div id="advList"></div>

      <div class="sectionline"></div>

      <h3>🧾 Видатки</h3>
      <div class="linebox">
        <div class="field">
          <label for="expNote">Назва видатку</label>
          <input id="expNote" placeholder="Наприклад: парковка, душ, дорога">
        </div>
        <div class="grid2">
          <div class="field">
            <label for="expAmount">Сума</label>
            <input id="expAmount" type="number" min="0" step="0.01" placeholder="25">
          </div>
          <div class="field">
            <label for="expCurrency">Валюта</label>
            <select id="expCurrency">
              <option value="EUR">Євро (€)</option>
              <option value="UAH">Гривня (₴)</option>
            </select>
          </div>
        </div>
        <button type="button" class="secondary" id="addExpense">+ Додати видаток</button>
      </div>
      <div id="expList"></div>

      <div class="sectionline"></div>

      <div class="field">
        <label for="notes">Примітка</label>
        <textarea id="notes" placeholder="Додаткова інформація про рейс"></textarea>
      </div>

      <div class="card" style="background:var(--field);margin:0">
        <h3>Розрахунок цього рейсу</h3>
        <div class="small">Зарплата до врахування авансів і видатків</div>
        <div id="liveSalary" style="font-size:20px;font-weight:800;margin:5px 0 12px">0,00 €</div>
        <div class="small">Залишок після авансів та з урахуванням видатків</div>
        <div id="liveBalance" style="font-size:23px;font-weight:800;color:var(--accent);margin:5px 0">0,00 €</div>
        <div id="liveUAH" class="small">У гривнях: 0,00 ₴</div>
      </div>

      <div class="buttons">
        <button type="submit" id="saveTrip">💾 Зберегти рейс</button>
        <button type="button" class="secondary" id="cancelEdit" hidden>Скасувати редагування</button>
      </div>
    </form>
  </section>

  <!-- ІСТОРІЯ -->
  <section class="card">
    <h2>📅 Історія рейсів</h2>
    <div class="grid2">
      <div class="field">
        <label for="filterFrom">Від дати</label>
        <input type="date" id="filterFrom">
      </div>
      <div class="field">
        <label for="filterTo">До дати</label>
        <input type="date" id="filterTo">
      </div>
    </div>
    <div class="buttons">
      <button type="button" id="applyFilter">Застосувати період</button>
      <button type="button" class="secondary" id="clearFilter">Усі рейси</button>
    </div>
    <div id="tripCount" class="small" style="margin:15px 0 10px">0 рейсів</div>
    <div id="tripList"></div>
  </section>

  <!-- РЕЗЕРВНІ КОПІЇ -->
  <section class="card">
    <h2>📦 Резервна копія</h2>
    <p class="small">Збережи файл із рейсами в «Файли» на iPhone. Це додатковий захист даних.</p>
    <div class="buttons">
      <button type="button" id="exportData">Експорт JSON</button>
      <button type="button" class="secondary" id="importButton">Імпорт JSON</button>
      <input type="file" id="importFile" accept=".json,application/json" hidden>
    </div>
    <div id="status">Завантаження даних…</div>
  </section>
</main>

<script>
"use strict";

const $ = id => document.getElementById(id);
const DB_NAME = "DriverSalaryLocalDB";
const DB_VERSION = 1;
const STORE_NAME = "trips";

let db = null;
let trips = [];
let draftAdvances = [];
let draftExpenses = [];
let filterActive = false;
let savedRate = Number(localStorage.getItem("driverSalaryRate") || 0);

function num(value) {
  const n = Number(value);
  return Number.isFinite(n) ? n : 0;
}

function money(value, currency = "EUR") {
  const n = Number.isFinite(Number(value)) ? Number(value) : 0;
  return new Intl.NumberFormat("uk-UA", {
    minimumFractionDigits: 2,
    maximumFractionDigits: 2
  }).format(n) + (currency === "UAH" ? " ₴" : " €");
}

function escapeHTML(value) {
  return String(value ?? "").replace(/[&<>"']/g, ch => ({
    "&": "&amp;",
    "<": "&lt;",
    ">": "&gt;",
    '"': "&quot;",
    "'": "&#39;"
  })[ch]);
}

function makeId() {
  return Date.now().toString(36) + Math.random().toString(36).slice(2, 9);
}

function convert(amount, from, to, rate) {
  amount = num(amount);
  if (from === to) return amount;
  if (!(rate > 0)) return 0;
  return from === "EUR" && to === "UAH"
    ? amount * rate
    : amount / rate;
}

function sumItems(items, targetCurrency, rate) {
  return (items || []).reduce((sum, item) => {
    return sum + convert(
      item.amount,
      item.currency || "EUR",
      targetCurrency,
      rate
    );
  }, 0);
}

function calc(t) {
  const currency = t.currency || "EUR";
  const rate = num(t.rate);

  // Зарплата водія від фрахту
  const salary = num(t.freight) * num(t.percent) / 100;

  // Аванси переводимо у валюту зарплати
  const adv = sumItems(t.advances, currency, rate);

  // Видатки переводимо у валюту зарплати
  const exp = sumItems(t.expenses, currency, rate);

  // Залишок: зарплата мінус аванси плюс компенсовані видатки
  const balance = salary - adv + exp;

  return { salary, adv, exp, balance, currency };
}


/* ЗБЕРЕЖЕННЯ НА ТЕЛЕФОНІ */

function openDatabase() {
  return new Promise((resolve, reject) => {
    if (!("indexedDB" in window)) {
      reject(new Error("IndexedDB недоступна"));
      return;
    }

    const request = indexedDB.open(DB_NAME, DB_VERSION);

    request.onupgradeneeded = event => {
      const database = event.target.result;
      if (!database.objectStoreNames.contains(STORE_NAME)) {
        database.createObjectStore(STORE_NAME, { keyPath: "id" });
      }
    };

    request.onsuccess = () => {
      db = request.result;
      db.onversionchange = () => db.close();
      resolve(db);
    };

    request.onerror = () => reject(request.error);
  });
}

function dbGetAll() {
  return new Promise((resolve, reject) => {
    const tx = db.transaction(STORE_NAME, "readonly");
    const request = tx.objectStore(STORE_NAME).getAll();
    request.onsuccess = () => resolve(request.result || []);
    request.onerror = () => reject(request.error);
  });
}

function dbPut(trip) {
  return new Promise((resolve, reject) => {
    const tx = db.transaction(STORE_NAME, "readwrite");
    tx.objectStore(STORE_NAME).put(trip);
    tx.oncomplete = () => resolve();
    tx.onerror = () => reject(tx.error);
    tx.onabort = () => reject(tx.error);
  });
}

function dbDelete(id) {
  return new Promise((resolve, reject) => {
    const tx = db.transaction(STORE_NAME, "readwrite");
    tx.objectStore(STORE_NAME).delete(id);
    tx.oncomplete = () => resolve();
    tx.onerror = () => reject(tx.error);
  });
}

async function loadTrips() {
  try {
    await openDatabase();
    trips = await dbGetAll();
    $("status").textContent = "Дані збережено локально на цьому пристрої.";
  } catch (error) {
    try {
      trips = JSON.parse(localStorage.getItem("driverTripsFallback") || "[]");
      $("status").textContent =
        "Резервне локальне збереження активне. Експортуй копію даних.";
    } catch {
      trips = [];
      $("status").textContent = "Не вдалося прочитати збережені дані.";
    }
  }

  render();
}

async function saveTripToStorage(trip) {
  if (db) {
    await dbPut(trip);
  } else {
    const index = trips.findIndex(t => t.id === trip.id);
    if (index >= 0) trips[index] = trip;
    else trips.push(trip);
    localStorage.setItem("driverTripsFallback", JSON.stringify(trips));
  }
}

async function deleteTripFromStorage(id) {
  if (db) {
    await dbDelete(id);
  } else {
    trips = trips.filter(t => String(t.id) !== String(id));
    localStorage.setItem("driverTripsFallback", JSON.stringify(trips));
  }
}

/* АВАНСИ ТА ВИДАТКИ */

function renderLineItems(type) {
  const items = type === "adv" ? draftAdvances : draftExpenses;
  const container = $(type === "adv" ? "advList" : "expList");
  const sign = type === "adv" ? "Аванс" : "Видаток";

  container.innerHTML = items.map((item, index) => `
    <div class="lineitem">
      <button type="button" class="danger"
        data-remove-line="${type}" data-index="${index}">✕</button>
      <strong>${escapeHTML(item.note || sign)}</strong>
      <div>${money(item.amount, item.currency)}</div>
    </div>
  `).join("");
}

function addLine(type) {
  const isAdv = type === "adv";
  const noteId = isAdv ? "advNote" : "expNote";
  const amountId = isAdv ? "advAmount" : "expAmount";
  const currencyId = isAdv ? "advCurrency" : "expCurrency";

  const amount = num($(amountId).value);
  if (!(amount > 0)) {
    alert("Введи суму, більшу за нуль.");
    return;
  }

  const item = {
    note: $(noteId).value.trim() || (isAdv ? "Аванс" : "Видаток"),
    amount,
    currency: $(currencyId).value
  };

  if (isAdv) {
    draftAdvances.push(item);
    $("advNote").value = "";
    $("advAmount").value = "";
    renderLineItems("adv");
  } else {
    draftExpenses.push(item);
    $("expNote").value = "";
    $("expAmount").value = "";
    renderLineItems("exp");
  }
  updateLive();
}

document.addEventListener("click", event => {
  const button = event.target.closest("[data-remove-line]");
  if (!button) return;

  const type = button.dataset.removeLine;
  const index = Number(button.dataset.index);

  if (type === "adv") draftAdvances.splice(index, 1);
  else draftExpenses.splice(index, 1);

  renderLineItems(type);
  updateLive();
});

$("addAdvance").addEventListener("click", () => addLine("adv"));
$("addExpense").addEventListener("click", () => addLine("exp"));

/* ПОТОЧНИЙ РОЗРАХУНОК */

function readForm() {
  return {
    date: $("tripDate").value,
    route: $("route").value.trim(),
    freight: num($("freight").value),
    currency: $("currency").value,
    percent: num($("percent").value),
    rate: num($("tripRate").value),
    advances: draftAdvances.map(x => ({ ...x })),
    expenses: draftExpenses.map(x => ({ ...x })),
    notes: $("notes").value.trim()
  };
}

function updateLive() {
  const t = readForm();
  const c = calc(t);
  const rate = num(t.rate);

  $("liveSalary").textContent = money(c.salary, c.currency);
  $("liveBalance").textContent = money(c.balance, c.currency);

  const balanceEUR = convert(c.balance, c.currency, "EUR", rate);
  const balanceUAH = convert(c.balance, c.currency, "UAH", rate);

  $("liveUAH").textContent =
    `У перерахунку: ${money(balanceEUR, "EUR")} · ${money(balanceUAH, "UAH")}`;
}

[
  "freight", "currency", "percent", "tripRate",
  "advAmount", "expAmount"
].forEach(id => $(id).addEventListener("input", updateLive));

/* ВЕРХНЯ СТАТИСТИКА */

function renderTopStats(list) {
  let salaryEUR = 0, salaryUAH = 0;
  let advEUR = 0, advUAH = 0;
  let expEUR = 0, expUAH = 0;

  list.forEach(t => {
    const c = calc(t);
    const rate = num(t.rate);

    salaryEUR += convert(c.salary, c.currency, "EUR", rate);
    salaryUAH += convert(c.salary, c.currency, "UAH", rate);

    advEUR += sumItems(t.advances, "EUR", rate);
    advUAH += sumItems(t.advances, "UAH", rate);
    expEUR += sumItems(t.expenses, "EUR", rate);
    expUAH += sumItems(t.expenses, "UAH", rate);
  });

  $("totalSalaryEUR").textContent = money(salaryEUR, "EUR");
  $("totalSalaryUAH").textContent = money(salaryUAH, "UAH");
  $("totalAdvEUR").textContent = money(advEUR, "EUR");
  $("totalAdvUAH").textContent = money(advUAH, "UAH");
  $("totalExpEUR").textContent = money(expEUR, "EUR");
  $("totalExpUAH").textContent = money(expUAH, "UAH");
}

/* КАРТКИ РЕЙСІВ */

function tripHTML(t) {
  const c = calc(t);
  const rate = num(t.rate);
  const balanceEUR = convert(c.balance, c.currency, "EUR", rate);
  const balanceUAH = convert(c.balance, c.currency, "UAH", rate);

  const showLines = (items, label) =>
    (items || []).map(item =>
      `<div>${escapeHTML(item.note || label)}: ${money(item.amount, item.currency || "EUR")}</div>`
    ).join("");

  return `
    <article class="trip">
      <div class="triptop">
        <div>
          <div class="triproute">${escapeHTML(t.route || "Рейс без назви")}</div>
          <div class="tripmeta">
            ${escapeHTML(t.date || "")} · Фрахт: ${money(t.freight, t.currency || "EUR")}
          </div>
        </div>
        <span class="pill">${escapeHTML(t.currency || "EUR")}</span>
      </div>

      <div class="tripbalance">${money(balanceEUR, "EUR")}</div>
      <div class="tripmeta">У гривнях: ${money(balanceUAH, "UAH")}</div>
      <div class="tripmeta">Курс рейсу: ${rate > 0 ? money(rate, "UAH") + " за EUR" : "не задано"}</div>

      ${(t.advances || []).length ? `
        <div class="tripdetails"><strong>Аванси</strong>
          ${showLines(t.advances, "Аванс")}
        </div>` : ""}

      ${(t.expenses || []).length ? `
        <div class="tripdetails"><strong>Видатки</strong>
          ${showLines(t.expenses, "Видаток")}
        </div>` : ""}

      ${t.notes ? `<div class="tripmeta">Примітка: ${escapeHTML(t.notes)}</div>` : ""}

      <div class="buttons">
        <button type="button" class="secondary" data-edit="${escapeHTML(t.id)}">Редагувати</button>
        <button type="button" class="danger" data-delete="${escapeHTML(t.id)}">Видалити</button>
      </div>
    </article>
  `;
}

/* СПИСОК І ПІДСУМКИ */

function render() {
  let list = [...trips].sort((a, b) =>
    (b.date || "").localeCompare(a.date || "")
  );

  if (filterActive) {
    const from = $("filterFrom").value;
    const to = $("filterTo").value;
    list = list.filter(t =>
      (!from || t.date >= from) &&
      (!to || t.date <= to)
    );
  }

  $("tripCount").textContent = `${list.length} рейсів`;
  renderTopStats(list);

  $("tripList").innerHTML = list.length
    ? list.map(tripHTML).join("")
    : `<div class="card empty">Рейсів поки немає.<br>Додай перший рейс вище.</div>`;
}

$("applyFilter").addEventListener("click", () => {
  filterActive = true;
  render();
});

$("clearFilter").addEventListener("click", () => {
  filterActive = false;
  $("filterFrom").value = "";
  $("filterTo").value = "";
  render();
});

/* ЗБЕРЕГТИ РЕЙС */

$("tripForm").addEventListener("submit", async event => {
  event.preventDefault();

  const t = readForm();

  if (!t.route) {
    alert("Вкажи маршрут рейсу.");
    return;
  }
  if (!(t.freight >= 0)) {
    alert("Перевір суму фрахту.");
    return;
  }
  if (!(t.rate > 0)) {
    alert("Вкажи курс євро до гривні.");
    return;
  }

  const editId = $("editId").value;
  t.id = editId || makeId();

  try {
    await saveTripToStorage(t);

    const index = trips.findIndex(item => String(item.id) === String(t.id));
    if (index >= 0) trips[index] = t;
    else trips.push(t);

    savedRate = t.rate;
    localStorage.setItem("driverSalaryRate", String(savedRate));

    resetForm();
    render();
    $("status").textContent = "Рейс успішно збережено на телефоні.";
    window.scrollTo({ top: 0, behavior: "smooth" });
  } catch (error) {
    alert("Не вдалося зберегти рейс. Спробуй ще раз та зроби резервну копію.");
    console.error(error);
  }
});

function resetForm() {
  $("tripForm").reset();
  $("editId").value = "";
  $("percent").value = "17";
  $("tripRate").value = savedRate > 0 ? savedRate : "";
  $("tripDate").value = new Date().toLocaleDateString("en-CA");
  $("formTitle").textContent = "➕ Додати рейс";
  $("saveTrip").textContent = "💾 Зберегти рейс";
  $("cancelEdit").hidden = true;

  draftAdvances = [];
  draftExpenses = [];
  renderLineItems("adv");
  renderLineItems("exp");
  updateLive();
}

$("cancelEdit").addEventListener("click", resetForm);

/* РЕДАГУВАННЯ ТА ВИДАЛЕННЯ */

document.addEventListener("click", async event => {
  const editButton = event.target.closest("[data-edit]");
  const deleteButton = event.target.closest("[data-delete]");

  if (editButton) {
    const trip = trips.find(t => String(t.id) === String(editButton.dataset.edit));
    if (!trip) return;

    $("editId").value = trip.id;
    $("tripDate").value = trip.date || "";
    $("route").value = trip.route || "";
    $("freight").value = trip.freight ?? "";
    $("currency").value = trip.currency || "EUR";
    $("percent").value = trip.percent ?? 17;
    $("tripRate").value = trip.rate ?? savedRate ?? "";
    $("notes").value = trip.notes || "";

    draftAdvances = (trip.advances || []).map(x => ({ ...x }));
    draftExpenses = (trip.expenses || []).map(x => ({ ...x }));
    renderLineItems("adv");
    renderLineItems("exp");
    updateLive();

    $("formTitle").textContent = "✏️ Редагувати рейс";
    $("saveTrip").textContent = "💾 Зберегти зміни";
    $("cancelEdit").hidden = false;

    window.scrollTo({ top: 0, behavior: "smooth" });
    return;
  }

  if (deleteButton) {
    const id = deleteButton.dataset.delete;
    if (!confirm("Точно видалити цей рейс?")) return;

    try {
      await deleteTripFromStorage(id);
      trips = trips.filter(t => String(t.id) !== String(id));
      render();
      $("status").textContent = "Рейс видалено.";
    } catch (error) {
      alert("Не вдалося видалити рейс.");
    }
  }
});

/* ЕКСПОРТ ТА ІМПОРТ */

$("exportData").addEventListener("click", () => {
  const backup = {
    app: "Мої рейси",
    version: 1,
    exportedAt: new Date().toISOString(),
    trips
  };

  const blob = new Blob(
    [JSON.stringify(backup, null, 2)],
    { type: "application/json;charset=utf-8" }
  );

  const url = URL.createObjectURL(blob);
  const link = document.createElement("a");
  link.href = url;
  link.download = `moi-reisy-${new Date().toISOString().slice(0, 10)}.json`;
  document.body.appendChild(link);
  link.click();
  link.remove();
  setTimeout(() => URL.revokeObjectURL(url), 1000);
});

$("importButton").addEventListener("click", () => $("importFile").click());

$("importFile").addEventListener("change", async event => {
  const file = event.target.files && event.target.files[0];
  if (!file) return;

  try {
    const parsed = JSON.parse(await file.text());
    const incoming = Array.isArray(parsed) ? parsed : parsed.trips;

    if (!Array.isArray(incoming)) {
      throw new Error("У файлі немає списку рейсів.");
    }

    if (!confirm("Імпорт додасть рейси до наявних. Продовжити?")) {
      event.target.value = "";
      return;
    }

    for (const item of incoming) {
      if (!item || item.id == null) continue;
      await saveTripToStorage(item);
      const index = trips.findIndex(t => String(t.id) === String(item.id));
      if (index >= 0) trips[index] = item;
      else trips.push(item);
    }

    if (!db) {
      localStorage.setItem("driverTripsFallback", JSON.stringify(trips));
    }

    render();
    $("status").textContent = "Імпорт завершено.";
    alert("Рейси успішно імпортовано.");
  } catch (error) {
    alert("Не вдалося імпортувати файл. Перевір, чи це правильна резервна копія.");
  }

  event.target.value = "";
});

/* ЗАПУСК */

resetForm();
loadTrips();
</script>
} catch (error) {
  alert("Помилка збереження: " + (error?.message || error));
  console.error("Помилка збереження рейсу:", error);
}
</script>

</body>
</html>
