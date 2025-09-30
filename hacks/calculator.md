---
title: JS Calculator
comments: true
hide: true
layout: opencs
description: A common way to become familiar with a language is to build a calculator.  This calculator shows off button with actions.
permalink: /calculator
---

<style>
  /* Calculator display area */
  .calculator-output {
    grid-column: span 4;
    grid-row: span 1;
    border-radius: 10px;
    padding: 0.25em;
    font-size: 20px;
    border: 5px solid black;
    display: flex;
    align-items: center;
    justify-content: flex-end; /* Right-align numbers */
  }

  canvas {
    filter: none;
  }

  /* Calculator container grid */
  .calculator-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr); /* 4 columns */
    gap: 10px;
    max-width: 400px;
    margin: 50px auto;
    z-index: 1;
    position: relative;
  }

  /* Button styles */
  .calculator-number,
  .calculator-operation,
  .calculator-clear,
  .calculator-equals {
    background: #2d7a78;
    color: #fff;
    font-size: 1.5rem;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    cursor: pointer;
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  /* Specific operation colors */
  .calculator-operation { background: #4682b4; }
  .calculator-clear { background: orange; }
  .calculator-equals { background: red; }

  /* Button hover effect */
  .calculator-number:hover,
  .calculator-operation:hover,
  .calculator-clear:hover,
  .calculator-equals:hover {
    opacity: 0.8;
  }

  /* History panel styling */
  .history {
    max-width: 400px;
    margin: 20px auto;
    padding: 10px;
    border: 2px solid #000;
    border-radius: 8px;
    background: #f8f8f8;
    color: #000;
    text-align: left;
    font-size: 14px;
    overflow-y: auto;
    max-height: 200px;
  }

  .history h3 {
    margin: 0 0 10px 0;
    text-align: center;
  }
</style>

<!-- Calculator UI -->
<div id="animation">
  <div class="calculator-container">
      <!-- Display output -->
      <div class="calculator-output" id="output">0</div>

      <!-- Row 1 -->
      <div class="calculator-number">1</div>
      <div class="calculator-number">2</div>
      <div class="calculator-number">3</div>
      <div class="calculator-operation">+</div>

      <!-- Row 2 -->
      <div class="calculator-number">4</div>
      <div class="calculator-number">5</div>
      <div class="calculator-number">6</div>
      <div class="calculator-operation">-</div>

      <!-- Row 3 -->
      <div class="calculator-number">7</div>
      <div class="calculator-number">8</div>
      <div class="calculator-number">9</div>
      <div class="calculator-operation">*</div>

      <!-- Row 4 -->
      <div class="calculator-clear">A/C</div>
      <div class="calculator-number">0</div>
      <div class="calculator-number">.</div>
      <div class="calculator-equals">=</div>

      <!-- Row 5: Additional operations -->
      <div class="calculator-operation">/</div>
      <div class="calculator-operation">//</div>
      <div class="calculator-operation">^</div>
      <div class="calculator-operation">√</div>
  </div>
</div>

<!-- History Panel -->
<div class="history" id="history">
  <h3>History</h3>
  <ul id="history-list"></ul>
</div>

<script>
/* --- Calculator Variables --- */
let firstNumber = null;       // Stores the first operand
let operator = null;          // Stores the selected operator
let nextReady = true;         // Determines if the next number starts fresh
let justCalculated = false;   // Tracks if last action was "="

/* --- DOM Elements --- */
const output = document.getElementById("output");
const numbers = document.querySelectorAll(".calculator-number");
const operations = document.querySelectorAll(".calculator-operation");
const clear = document.querySelectorAll(".calculator-clear");
const equals = document.querySelectorAll(".calculator-equals");
const historyList = document.getElementById("history-list");

/* --- Number Button Handling --- */
numbers.forEach(button => {
  button.addEventListener("click", function() {
    inputNumber(button.textContent);
  });
});

/* Function to handle number input */
function inputNumber(value) {
  if (nextReady || justCalculated) {
    // Start fresh for a new number
    output.innerHTML = value;
    nextReady = false;

    if (justCalculated) {
      // Reset state after a previous calculation
      firstNumber = null;
      operator = null;
      justCalculated = false;
    }
  } else {
    // Append number to current display
    output.innerHTML += value;
  }
}

/* --- Operation Button Handling --- */
operations.forEach(button => {
  button.addEventListener("click", function() {
    handleOperation(button.textContent);
  });
});

/* Function to handle operations */
function handleOperation(choice) {
  if (choice === "√") {
    // Single-number square root operation
    let val = parseFloat(output.innerHTML);
    output.innerHTML = Math.sqrt(val).toString();
    addHistory(`√${val} = ${output.innerHTML}`);
    nextReady = true;
    justCalculated = true;
    return;
  }

  // For multi-number operations
  if (firstNumber === null) {
    firstNumber = parseFloat(output.innerHTML);
  } else if (!nextReady) {
    firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
    output.innerHTML = firstNumber.toString();
  }

  operator = choice;
  nextReady = true;
  justCalculated = false;
}

/* --- Calculator Logic --- */
function calculate(first, second) {
  let result = 0;
  switch (operator) {
    case "+": result = first + second; break;
    case "-": result = first - second; break;
    case "*": result = first * second; break;
    case "/": result = first / second; break;
    case "//": result = Math.floor(first / second); break;
    case "^": result = Math.pow(first, second); break;
    default: break;
  }
  
  // Round to 10 decimal places to fix floating-point issues
  result = parseFloat(result.toFixed(10));
  
  addHistory(`${first} ${operator} ${second} = ${result}`);
  return result;
}


/* --- Equals Button Handling --- */
equals.forEach(button => {
  button.addEventListener("click", function() {
    handleEquals();
  });
});

function handleEquals() {
  if (firstNumber !== null && operator !== null) {
    firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
    output.innerHTML = firstNumber.toString();
    nextReady = true;
    operator = null;
    justCalculated = true;
  }
}

/* --- Clear Button Handling --- */
clear.forEach(button => {
  button.addEventListener("click", function() {
    clearCalc();
  });
});

/* Function to clear calculator and history */
function clearCalc() {
  firstNumber = null;
  operator = null;
  nextReady = true;
  justCalculated = false;
  output.innerHTML = "0";
  historyList.innerHTML = "";
}

/* --- History Tracking --- */
function addHistory(entry) {
  let li = document.createElement("li");
  li.textContent = entry;
  historyList.appendChild(li);
}
</script>

<!-- Vanta animations -->
<script src="{{site.baseurl}}/assets/js/three.r119.min.js"></script>
<script src="{{site.baseurl}}/assets/js/vanta.halo.min.js"></script>
<script src="{{site.baseurl}}/assets/js/vanta.birds.min.js"></script>
<script src="{{site.baseurl}}/assets/js/vanta.net.min.js"></script>
<script src="{{site.baseurl}}/assets/js/vanta.rings.min.js"></script>

<script>
/* --- Initialize Random Vanta Background --- */
var vantaInstances = { halo: VANTA.HALO, birds: VANTA.BIRDS, net: VANTA.NET, rings: VANTA.RINGS };
var vantaInstance = vantaInstances[Object.keys(vantaInstances)[Math.floor(Math.random() * Object.keys(vantaInstances).length)]];
vantaInstance({ el: "#animation", mouseControls: true, touchControls: true, gyroControls: false });
</script>

<!-- Footer with changes -->
<footer>
  <h3>Changes from the Original Calculator</h3>
  <ul style="list-style-type: none; padding: 0;">
    <li>✅ Hack 0: Right justified the calculator output.</li>
    <li>✅ Hack 1: Fixed handling for small, big, and decimal numbers.</li>
    <li>✅ Hack 2: Added missing math operations: <strong>division (/), integer division (//), and exponents (^)</strong>.</li>
    <li>✅ Hack 3: Implemented single-number operation: <strong>square root (√)</strong>.</li>
    <li>📝 Added a <strong>history panel</strong> to track past expressions and results.</li>
  </ul>
</footer>
