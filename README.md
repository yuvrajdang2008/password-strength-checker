# password-strength-checker
A password checker program validates password strength and security by analyzing user input against defined criteria like minimum length, uppercase/lowercase letters, digits, and special characters. Typically written in Python, the code uses loops, conditional statements, and string character counters to assign a strength score, offering feedback.
<p style="text-align:center; font-size:12px; opacity:0.6;">
© 2026 | Built by Yuvraj
</p>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Password Strength Checker</title>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
  color: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

.container {
  background: #111;
  padding: 20px;
  width: 100%;
  max-width: 400px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
}

h2 {
  text-align: center;
  margin-bottom: 20px;
}

.input-box {
  position: relative;
}

input {
  width: 100%;
  padding: 12px;
  font-size: 16px;
  border-radius: 8px;
  border: none;
  outline: none;
}

.toggle {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  cursor: pointer;
  font-size: 14px;
  color: #00e5ff;
}

.strength-bar {
  height: 8px;
  background: #333;
  border-radius: 5px;
  margin: 15px 0;
  overflow: hidden;
}

.strength-bar div {
  height: 100%;
  width: 0%;
  transition: width 0.3s ease;
}

.rules {
  font-size: 14px;
  margin-top: 10px;
}

.rules p {
  margin: 5px 0;
}

.result {
  text-align: center;
  font-weight: bold;
  margin-top: 10px;
}

.tip {
  font-size: 13px;
  text-align: center;
  margin-top: 10px;
  opacity: 0.8;
}
</style>
</head>

<body>

<div class="container">
  <h2>Password Strength 🔐</h2>

  <div class="input-box">
    <input type="password" id="password" placeholder="Enter password" onkeyup="checkPassword()">
    <span class="toggle" onclick="togglePassword()">Show</span>
  </div>

  <div class="strength-bar">
    <div id="bar"></div>
  </div>

  <div class="rules">
    <p id="len8">❌ At least 8 characters</p>
    <p id="len12">❌ At least 12 characters</p>
    <p id="upper">❌ Uppercase letter</p>
    <p id="lower">❌ Lowercase letter</p>
    <p id="number">❌ Number</p>
    <p id="special">❌ Special character</p>
  </div>

  <div class="result" id="result"></div>
  <div class="tip" id="crack"></div>
</div>

<script>
const commonPasswords = ["123456", "password", "123456789", "qwerty"];

function togglePassword() {
  const input = document.getElementById("password");
  input.type = input.type === "password" ? "text" : "password";
}

function checkPassword() {
  const pwd = document.getElementById("password").value;
  let score = 0;

  setRule("len8", pwd.length >= 8);
  setRule("len12", pwd.length >= 12);
  setRule("upper", /[A-Z]/.test(pwd));
  setRule("lower", /[a-z]/.test(pwd));
  setRule("number", /[0-9]/.test(pwd));
  setRule("special", /[^A-Za-z0-9]/.test(pwd));

  if (pwd.length >= 8) score++;
  if (pwd.length >= 12) score++;
  if (/[A-Z]/.test(pwd)) score++;
  if (/[a-z]/.test(pwd)) score++;
  if (/[0-9]/.test(pwd)) score++;
  if (/[^A-Za-z0-9]/.test(pwd)) score++;

  const bar = document.getElementById("bar");
  bar.style.width = (score / 6) * 100 + "%";

  let result = document.getElementById("result");
  let crack = document.getElementById("crack");

  if (commonPasswords.includes(pwd)) {
    result.textContent = "Very Weak ❌ (Common Password)";
    bar.style.background = "red";
    crack.textContent = "Can be cracked instantly.";
    return;
  }

  if (score <= 2) {
    result.textContent = "Weak ❌";
    bar.style.background = "red";
    crack.textContent = "Crack time: seconds to minutes";
  } else if (score <= 4) {
    result.textContent = "Medium ⚠️";
    bar.style.background = "orange";
    crack.textContent = "Crack time: hours to days";
  } else {
    result.textContent = "Strong ✅";
    bar.style.background = "lime";
    crack.textContent = "Crack time: years (with current tech)";
  }
}

function setRule(id, condition) {
  const el = document.getElementById(id);
  el.textContent = condition ? "✔️ " + el.textContent.slice(2) : "❌ " + el.textContent.slice(2);
}
</script>

</body>
</html>
