<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Finance Analyzer</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet"/>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #f7f6f3;
    --surface: #ffffff;
    --border: #e4e2dc;
    --text: #1a1916;
    --muted: #7a7870;
    --accent: #1a1916;
    --green: #1d6b4a;
    --green-bg: #eaf3de;
    --amber: #854f0b;
    --amber-bg: #faeeda;
    --red: #a32d2d;
    --red-bg: #fcebeb;
    --radius: 14px;
  }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    padding: 2rem 1rem 4rem;
  }

  .wrap { max-width: 720px; margin: 0 auto; }

  header { text-align: center; margin-bottom: 3rem; }
  header h1 {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(2rem, 5vw, 3rem);
    font-weight: 400;
    letter-spacing: -0.02em;
    line-height: 1.1;
    margin-bottom: 0.5rem;
  }
  header p { color: var(--muted); font-size: 1rem; font-weight: 300; }

  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 1.75rem;
    margin-bottom: 1rem;
  }

  .card-title {
    font-size: 0.75rem;
    font-weight: 500;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 1.25rem;
  }

  .field-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0.75rem;
    margin-bottom: 0.75rem;
  }
  @media(max-width: 500px) { .field-row { grid-template-columns: 1fr; } }

  .field { display: flex; flex-direction: column; gap: 0.35rem; }
  .field label { font-size: 0.8rem; color: var(--muted); font-weight: 400; }

  .field input, .field select, .field textarea {
    font-family: 'DM Sans', sans-serif;
    font-size: 0.95rem;
    font-weight: 400;
    color: var(--text);
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 0.6rem 0.85rem;
    outline: none;
    transition: border-color 0.15s;
    width: 100%;
  }
  .field input:focus, .field textarea:focus { border-color: var(--text); }
  .field input::placeholder, .field textarea::placeholder { color: #bbb; }

  .expense-list { display: flex; flex-direction: column; gap: 0.6rem; }
  .expense-item {
    display: grid;
    grid-template-columns: 1fr auto auto;
    gap: 0.5rem;
    align-items: center;
  }
  .expense-item input { margin: 0; }
  .expense-item .amount { max-width: 110px; }
  .del-btn {
    background: none; border: none; cursor: pointer;
    color: var(--muted); font-size: 1.1rem; padding: 0 4px;
    transition: color 0.15s;
  }
  .del-btn:hover { color: var(--red); }

  .add-btn {
    margin-top: 0.75rem;
    background: none;
    border: 1px dashed var(--border);
    border-radius: 8px;
    padding: 0.55rem 1rem;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.85rem;
    color: var(--muted);
    cursor: pointer;
    width: 100%;
    transition: border-color 0.15s, color 0.15s;
  }
  .add-btn:hover { border-color: var(--text); color: var(--text); }

  .analyze-btn {
    width: 100%;
    background: var(--text);
    color: #fff;
    border: none;
    border-radius: var(--radius);
    padding: 1rem;
    font-family: 'DM Serif Display', serif;
    font-size: 1.1rem;
    font-style: italic;
    cursor: pointer;
    margin-top: 0.5rem;
    transition: opacity 0.2s, transform 0.1s;
    letter-spacing: 0.01em;
  }
  .analyze-btn:hover { opacity: 0.88; }
  .analyze-btn:active { transform: scale(0.99); }
  .analyze-btn:disabled { opacity: 0.5; cursor: not-allowed; }

  /* Results */
  #results { display: none; margin-top: 2rem; }

  .score-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 2rem 1.75rem;
    margin-bottom: 1rem;
    display: flex;
    align-items: center;
    gap: 2rem;
  }
  .score-ring {
    flex-shrink: 0;
    width: 88px; height: 88px;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    flex-direction: column;
    border: 3px solid var(--border);
    position: relative;
  }
  .score-ring .score-num {
    font-family: 'DM Serif Display', serif;
    font-size: 2rem;
    line-height: 1;
  }
  .score-ring .score-label { font-size: 0.65rem; color: var(--muted); letter-spacing: 0.05em; text-transform: uppercase; }
  .score-info h2 { font-family: 'DM Serif Display', serif; font-size: 1.4rem; font-weight: 400; margin-bottom: 0.3rem; }
  .score-info p { color: var(--muted); font-size: 0.9rem; line-height: 1.5; }

  .chips { display: flex; flex-wrap: wrap; gap: 0.5rem; margin-top: 1rem; }
  .chip {
    font-size: 0.78rem;
    font-weight: 500;
    padding: 0.3rem 0.75rem;
    border-radius: 99px;
  }
  .chip.green { background: var(--green-bg); color: var(--green); }
  .chip.amber { background: var(--amber-bg); color: var(--amber); }
  .chip.red { background: var(--red-bg); color: var(--red); }

  .insight-section { margin-bottom: 1rem; }
  .insight-section .card-title { margin-bottom: 1rem; }

  .insight-block {
    border-left: 2px solid var(--border);
    padding: 0.6rem 1rem;
    margin-bottom: 0.85rem;
    font-size: 0.92rem;
    line-height: 1.6;
    color: var(--text);
  }
  .insight-block.good { border-color: var(--green); }
  .insight-block.warn { border-color: #e9a500; }
  .insight-block.bad { border-color: var(--red); }

  .action-item {
    display: flex; align-items: flex-start; gap: 0.75rem;
    padding: 0.85rem 0;
    border-bottom: 1px solid var(--border);
    font-size: 0.92rem;
    line-height: 1.5;
  }
  .action-item:last-child { border-bottom: none; }
  .action-num {
    flex-shrink: 0;
    width: 24px; height: 24px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 0.72rem;
    font-weight: 500;
    color: var(--muted);
    margin-top: 1px;
  }

  .breakdown-bars { display: flex; flex-direction: column; gap: 0.75rem; }
  .bar-row { display: grid; grid-template-columns: 130px 1fr 60px; align-items: center; gap: 0.75rem; }
  .bar-label { font-size: 0.82rem; color: var(--muted); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .bar-track { height: 6px; background: var(--bg); border-radius: 99px; overflow: hidden; border: 1px solid var(--border); }
  .bar-fill { height: 100%; border-radius: 99px; background: var(--text); transition: width 0.6s ease; }
  .bar-fill.green { background: var(--green); }
  .bar-fill.amber { background: #e9a500; }
  .bar-fill.red { background: var(--red); }
  .bar-pct { font-size: 0.8rem; font-weight: 500; text-align: right; }

  .loading-state {
    text-align: center;
    padding: 3rem;
    color: var(--muted);
    font-style: italic;
    font-family: 'DM Serif Display', serif;
    font-size: 1.1rem;
    display: none;
  }
  .loading-dot {
    display: inline-block;
    animation: blink 1.2s infinite;
  }
  .loading-dot:nth-child(2) { animation-delay: 0.2s; }
  .loading-dot:nth-child(3) { animation-delay: 0.4s; }
  @keyframes blink { 0%,80%,100%{opacity:0.2} 40%{opacity:1} }

  .error-msg {
    background: var(--red-bg);
    color: var(--red);
    border-radius: 8px;
    padding: 0.75rem 1rem;
    font-size: 0.88rem;
    margin-top: 0.75rem;
    display: none;
  }

  .reset-btn {
    display: block;
    margin: 1.5rem auto 0;
    background: none;
    border: 1px solid var(--border);
    border-radius: 99px;
    padding: 0.5rem 1.5rem;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.85rem;
    color: var(--muted);
    cursor: pointer;
    transition: color 0.15s, border-color 0.15s;
  }
  .reset-btn:hover { color: var(--text); border-color: var(--text); }
</style>
</head>
<body>
<div class="wrap">
  <header>
    <h1>Your Financial Health,<br/><em>analyzed.</em></h1>
    <p>Enter your numbers. Get real insights in seconds.</p>
  </header>

  <!-- INPUT FORM -->
  <div id="form-section">
    <div class="card">
      <div class="card-title">Income</div>
      <div class="field-row">
        <div class="field">
          <label>Monthly take-home income (₹)</label>
          <input type="number" id="income" placeholder="e.g. 75000" min="0"/>
        </div>
        <div class="field">
          <label>Other income / side hustle (₹)</label>
          <input type="number" id="other-income" placeholder="e.g. 10000" min="0"/>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-title">Monthly Expenses</div>
      <div class="expense-list" id="expense-list">
        <div class="expense-item">
          <input type="text" placeholder="Category (e.g. Rent)" value="Rent"/>
          <input type="number" class="amount" placeholder="Amount ₹" value=""/>
          <button class="del-btn" onclick="removeExpense(this)">×</button>
        </div>
        <div class="expense-item">
          <input type="text" placeholder="Category" value="Food & Groceries"/>
          <input type="number" class="amount" placeholder="Amount ₹" value=""/>
          <button class="del-btn" onclick="removeExpense(this)">×</button>
        </div>
        <div class="expense-item">
          <input type="text" placeholder="Category" value="Transport"/>
          <input type="number" class="amount" placeholder="Amount ₹" value=""/>
          <button class="del-btn" onclick="removeExpense(this)">×</button>
        </div>
        <div class="expense-item">
          <input type="text" placeholder="Category" value="Entertainment"/>
          <input type="number" class="amount" placeholder="Amount ₹" value=""/>
          <button class="del-btn" onclick="removeExpense(this)">×</button>
        </div>
      </div>
      <button class="add-btn" onclick="addExpense()">+ Add category</button>
    </div>

    <div class="card">
      <div class="card-title">Goals & Context</div>
      <div class="field-row">
        <div class="field">
          <label>Current savings (₹)</label>
          <input type="number" id="savings" placeholder="e.g. 150000" min="0"/>
        </div>
        <div class="field">
          <label>Monthly savings target (₹)</label>
          <input type="number" id="savings-goal" placeholder="e.g. 15000" min="0"/>
        </div>
      </div>
      <div class="field" style="margin-top:0.75rem">
        <label>What's your biggest financial goal or worry?</label>
        <textarea id="goal" rows="2" placeholder="e.g. Build a 6-month emergency fund, save for a house, pay off loan..."></textarea>
      </div>
    </div>

    <div id="error-msg" class="error-msg"></div>
    <button class="analyze-btn" onclick="analyze()">Analyze my finances →</button>
  </div>

  <div class="loading-state" id="loading">
    Crunching your numbers<span class="loading-dot">.</span><span class="loading-dot">.</span><span class="loading-dot">.</span>
  </div>

  <!-- RESULTS -->
  <div id="results">
    <div class="score-card" id="score-card">
      <div class="score-ring" id="score-ring">
        <span class="score-num" id="score-num">—</span>
        <span class="score-label">/ 100</span>
      </div>
      <div class="score-info">
        <h2 id="score-title">—</h2>
        <p id="score-desc">—</p>
        <div class="chips" id="score-chips"></div>
      </div>
    </div>

    <div class="card insight-section">
      <div class="card-title">Spending Breakdown</div>
      <div class="breakdown-bars" id="breakdown-bars"></div>
    </div>

    <div class="card insight-section">
      <div class="card-title">Key Insights</div>
      <div id="insights-list"></div>
    </div>

    <div class="card insight-section">
      <div class="card-title">Action Plan</div>
      <div id="actions-list"></div>
    </div>

    <button class="reset-btn" onclick="reset()">Analyze different numbers</button>
  </div>
</div>

<script>
function addExpense() {
  const list = document.getElementById('expense-list');
  const div = document.createElement('div');
  div.className = 'expense-item';
  div.innerHTML = `
    <input type="text" placeholder="Category"/>
    <input type="number" class="amount" placeholder="Amount ₹"/>
    <button class="del-btn" onclick="removeExpense(this)">×</button>
  `;
  list.appendChild(div);
}

function removeExpense(btn) {
  const items = document.querySelectorAll('.expense-item');
  if (items.length > 1) btn.parentElement.remove();
}

function getExpenses() {
  const items = document.querySelectorAll('.expense-item');
  const expenses = [];
  items.forEach(item => {
    const inputs = item.querySelectorAll('input');
    const cat = inputs[0].value.trim();
    const amt = parseFloat(inputs[1].value) || 0;
    if (cat && amt > 0) expenses.push({ category: cat, amount: amt });
  });
  return expenses;
}

function showError(msg) {
  const el = document.getElementById('error-msg');
  el.textContent = msg;
  el.style.display = 'block';
}

function hideError() {
  document.getElementById('error-msg').style.display = 'none';
}

async function analyze() {
  hideError();
  const income = parseFloat(document.getElementById('income').value) || 0;
  const otherIncome = parseFloat(document.getElementById('other-income').value) || 0;
  const savings = parseFloat(document.getElementById('savings').value) || 0;
  const savingsGoal = parseFloat(document.getElementById('savings-goal').value) || 0;
  const goal = document.getElementById('goal').value.trim();
  const expenses = getExpenses();

  if (!income) { showError('Please enter your monthly income to continue.'); return; }
  if (expenses.length === 0) { showError('Please add at least one expense category.'); return; }

  const totalExpenses = expenses.reduce((s, e) => s + e.amount, 0);
  const totalIncome = income + otherIncome;

  document.getElementById('form-section').style.display = 'none';
  document.getElementById('loading').style.display = 'block';

  const prompt = `You are a personal finance advisor. Analyze the following financial data and respond ONLY with a valid JSON object. No explanation outside the JSON.

Financial Data:
- Monthly take-home income: ₹${income}
- Other monthly income: ₹${otherIncome}
- Total monthly income: ₹${totalIncome}
- Current savings: ₹${savings}
- Monthly savings target: ₹${savingsGoal}
- Financial goal: ${goal || 'Not specified'}
- Monthly expenses breakdown:
${expenses.map(e => `  * ${e.category}: ₹${e.amount}`).join('\n')}
- Total monthly expenses: ₹${totalExpenses}
- Net monthly surplus/deficit: ₹${totalIncome - totalExpenses}

Respond with this exact JSON structure:
{
  "score": <integer 0-100 representing financial health>,
  "scoreTitle": "<2-4 word title like 'Financially Stable' or 'Needs Attention'>",
  "scoreDesc": "<1-2 sentence honest overall summary>",
  "chips": [
    {"label": "<short label>", "type": "green|amber|red"}
  ],
  "insights": [
    {"text": "<specific insight with actual numbers>", "type": "good|warn|bad"}
  ],
  "actions": [
    "<specific actionable step with numbers>"
  ]
}

Rules:
- score must be honest and data-driven (not artificially high)
- Include 3-4 chips (key financial metrics at a glance)
- Include 3-5 insights, each referencing actual numbers from the data
- Include 4-5 concrete action steps with specific numbers/amounts
- Use Indian Rupee context (₹)
- Be direct, specific, and genuinely helpful`;

  try {
    const resp = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        model: 'claude-sonnet-4-20250514',
        max_tokens: 1000,
        messages: [{ role: 'user', content: prompt }]
      })
    });

    const data = await resp.json();
    const text = data.content?.find(b => b.type === 'text')?.text || '';
    const clean = text.replace(/```json|```/g, '').trim();
    const result = JSON.parse(clean);

    document.getElementById('loading').style.display = 'none';
    renderResults(result, expenses, totalIncome, totalExpenses);

  } catch(e) {
    document.getElementById('loading').style.display = 'none';
    document.getElementById('form-section').style.display = 'block';
    showError('Something went wrong analyzing your data. Please try again.');
  }
}

function renderResults(r, expenses, totalIncome, totalExpenses) {
  // Score
  const score = Math.min(100, Math.max(0, r.score));
  document.getElementById('score-num').textContent = score;
  document.getElementById('score-title').textContent = r.scoreTitle;
  document.getElementById('score-desc').textContent = r.scoreDesc;

  const ring = document.getElementById('score-ring');
  ring.style.borderColor = score >= 70 ? '#1d6b4a' : score >= 45 ? '#e9a500' : '#a32d2d';
  document.getElementById('score-num').style.color = score >= 70 ? '#1d6b4a' : score >= 45 ? '#e9a500' : '#a32d2d';

  // Chips
  const chipsEl = document.getElementById('score-chips');
  chipsEl.innerHTML = (r.chips || []).map(c =>
    `<span class="chip ${c.type}">${c.label}</span>`
  ).join('');

  // Breakdown bars
  const barsEl = document.getElementById('breakdown-bars');
  const sorted = [...expenses].sort((a,b) => b.amount - a.amount);
  barsEl.innerHTML = sorted.map(e => {
    const pct = totalIncome > 0 ? Math.round((e.amount / totalIncome) * 100) : 0;
    const color = pct > 40 ? 'red' : pct > 20 ? 'amber' : 'green';
    return `
      <div class="bar-row">
        <span class="bar-label">${e.category}</span>
        <div class="bar-track"><div class="bar-fill ${color}" style="width:${Math.min(pct,100)}%"></div></div>
        <span class="bar-pct">${pct}%</span>
      </div>`;
  }).join('');

  // Insights
  const insightsEl = document.getElementById('insights-list');
  insightsEl.innerHTML = (r.insights || []).map(i =>
    `<div class="insight-block ${i.type}">${i.text}</div>`
  ).join('');

  // Actions
  const actionsEl = document.getElementById('actions-list');
  actionsEl.innerHTML = (r.actions || []).map((a, i) =>
    `<div class="action-item"><span class="action-num">${i+1}</span><span>${a}</span></div>`
  ).join('');

  document.getElementById('results').style.display = 'block';
}

function reset() {
  document.getElementById('results').style.display = 'none';
  document.getElementById('form-section').style.display = 'block';
}
</script>
</body>
</html>
