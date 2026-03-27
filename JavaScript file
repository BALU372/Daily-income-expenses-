// Elements
const descInput = document.getElementById('desc');
const amountInput = document.getElementById('amount');
const typeInput = document.getElementById('type');
const addBtn = document.getElementById('addBtn');
const tableBody = document.querySelector('#transactionTable tbody');
const totalIncomeEl = document.getElementById('totalIncome');
const totalExpenseEl = document.getElementById('totalExpense');
const balanceEl = document.getElementById('balance');

// Load transactions from localStorage
let transactions = JSON.parse(localStorage.getItem('transactions')) || [];
transactions.forEach(t => addTransactionToTable(t));
updateSummary();

// Add transaction
addBtn.addEventListener('click', () => {
    const desc = descInput.value.trim();
    const amount = parseFloat(amountInput.value);
    const type = typeInput.value;

    if(desc === '' || isNaN(amount)) return alert('Enter valid data');

    const transaction = { desc, amount, type };
    transactions.push(transaction);
    localStorage.setItem('transactions', JSON.stringify(transactions));
    
    addTransactionToTable(transaction);
    updateSummary();

    descInput.value = '';
    amountInput.value = '';
});

// Add transaction row to table
function addTransactionToTable(transaction) {
    const tr = document.createElement('tr');

    tr.innerHTML = `
        <td>${transaction.desc}</td>
        <td>${transaction.amount}</td>
        <td class="${transaction.type}">${transaction.type}</td>
        <td><button class="deleteBtn">Delete</button></td>
    `;

    tr.querySelector('.deleteBtn').addEventListener('click', () => {
        tableBody.removeChild(tr);
        transactions = transactions.filter(t => t !== transaction);
        localStorage.setItem('transactions', JSON.stringify(transactions));
        updateSummary();
    });

    tableBody.appendChild(tr);
}

// Update totals
function updateSummary() {
    let totalIncome = 0;
    let totalExpense = 0;

    transactions.forEach(t => {
        if(t.type === 'income') totalIncome += t.amount;
        else totalExpense += t.amount;
    });

    totalIncomeEl.textContent = totalIncome;
    totalExpenseEl.textContent = totalExpense;
    balanceEl.textContent = (totalIncome - totalExpense);
}
