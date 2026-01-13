<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>محفظتي</title>

<style>
body{
    margin:0;
    font-family: Arial, sans-serif;
    background:#f2f2f2;
}
.app{
    max-width:420px;
    margin:auto;
    background:#fff;
    min-height:100vh;
}
.header{
    background:linear-gradient(135deg,#4CAF50,#2e7d32);
    color:#fff;
    padding:20px;
    text-align:center;
}
.balance{
    font-size:28px;
    margin-top:10px;
}
.card{
    margin:15px;
    padding:15px;
    border-radius:12px;
    background:#fafafa;
    box-shadow:0 2px 6px rgba(0,0,0,.1);
}
.card h3{
    margin:0 0 10px;
}
input, button{
    width:100%;
    padding:12px;
    margin-top:8px;
    border-radius:8px;
    border:1px solid #ccc;
    font-size:16px;
}
button{
    background:#4CAF50;
    color:#fff;
    border:none;
}
button.send{
    background:#2196F3;
}
button.withdraw{
    background:#f44336;
}
.tx{
    display:flex;
    justify-content:space-between;
    margin:8px 0;
    font-size:14px;
}
.tx.plus{color:green;}
.tx.minus{color:red;}
.footer{
    text-align:center;
    padding:10px;
    font-size:12px;
    color:#888;
}
</style>
</head>

<body>
<div class="app">

    <div class="header">
        <h2>💳 محفظتي</h2>
        <div class="balance" id="balance">0.00 MAD</div>
    </div>

    <div class="card">
        <h3>➕ شحن الرصيد</h3>
        <input type="number" id="addAmount" placeholder="أدخل المبلغ">
        <button onclick="addMoney()">شحن</button>
    </div>

    <div class="card">
        <h3>📤 إرسال</h3>
        <input type="text" id="sendTo" placeholder="رقم أو اسم المستلم">
        <input type="number" id="sendAmount" placeholder="المبلغ">
        <button class="send" onclick="sendMoney()">إرسال</button>
    </div>

    <div class="card">
        <h3>🏧 سحب</h3>
        <input type="number" id="withdrawAmount" placeholder="المبلغ">
        <button class="withdraw" onclick="withdrawMoney()">سحب</button>
    </div>

    <div class="card">
        <h3>📜 المعاملات</h3>
        <div id="transactions"></div>
    </div>

    <div class="footer">
        © 2026 محفظة HTML
    </div>

</div>

<script>
let balance = 0;

function updateBalance(){
    document.getElementById("balance").innerText = balance.toFixed(2) + " MAD";
}

function addTx(text, amount, type){
    const tx = document.createElement("div");
    tx.className = "tx " + type;
    tx.innerHTML = `<span>${text}</span><span>${amount}</span>`;
    document.getElementById("transactions").prepend(tx);
}

function addMoney(){
    let amt = Number(document.getElementById("addAmount").value);
    if(amt > 0){
        balance += amt;
        updateBalance();
        addTx("شحن رصيد", "+"+amt, "plus");
    }
}

function sendMoney(){
    let amt = Number(document.getElementById("sendAmount").value);
    let to = document.getElementById("sendTo").value;
    if(amt > 0 && amt <= balance){
        balance -= amt;
        updateBalance();
        addTx("إرسال إلى " + to, "-"+amt, "minus");
    }
}

function withdrawMoney(){
    let amt = Number(document.getElementById("withdrawAmount").value);
    if(amt > 0 && amt <= balance){
        balance -= amt;
        updateBalance();
        addTx("سحب", "-"+amt, "minus");
    }
}
</script>

</body>
</html>
