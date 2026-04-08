---
title: JS Calculator
comments: true
hide: true
layout: opencs
description: A common way to become familiar with a language is to build a calculator.  This calculator shows off button with actions.
permalink: /calculator
---

<style>
  .calculator-output {
    grid-column: span 4;
    grid-row: span 1;
    border-radius: 16px;
    padding: 12px 20px;
    font-size: 48px;
    font-weight: 300;
    border: none;
    background: #1c1c1e;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    box-shadow: inset 0 2px 8px rgba(0,0,0,0.5);
    letter-spacing: -1px;
  }

  canvas {
    filter: none;
  }

  .calculator-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
    max-width: 420px;
    margin: 30px auto;
    z-index: 1;
    position: relative;
    background: #1a1a1a;
    padding: 20px;
    border-radius: 24px;
    box-shadow: 0 8px 32px rgba(0,0,0,0.6);
  }

  .calculator-number,
  .calculator-operation,
  .calculator-clear,
  .calculator-equals {
    background: #2c2c2e;
    color: #fff;
    font-size: 1.4rem;
    font-weight: 500;
    padding: 18px;
    border-radius: 16px;
    text-align: center;
    cursor: pointer;
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: opacity 0.1s, transform 0.1s;
  }

  .calculator-operation {
    background: #ff9500;
    box-shadow: 0 0 10px rgba(255,149,0,0.3);
  }

  .calculator-clear { background: #636366; }

  .calculator-equals {
    background: #34c759;
    box-shadow: 0 0 10px rgba(52,199,89,0.3);
  }

  .calculator-number:hover {
    opacity: 0.75;
    box-shadow: 0 0 8px rgba(255,255,255,0.1);
  }

  .calculator-operation:hover,
  .calculator-equals:hover {
    opacity: 0.85;
  }

  .calculator-clear:hover {
    opacity: 0.8;
  }

  .calculator-analyze {
    grid-column: span 2;
    background: #ff9500;
    color: #fff;
    font-size: 1.4rem;
    font-weight: 500;
    padding: 18px;
    border-radius: 16px;
    text-align: center;
    cursor: pointer;
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
    box-shadow: 0 0 10px rgba(255,149,0,0.3);
    transition: opacity 0.1s;
  }

  .calculator-analyze:hover {
    opacity: 0.85;
  }

  .calculator-clear-history {
    grid-column: span 4;
    background: #636366 !important;
    box-shadow: none !important;
  }

  .calculator-title {
    text-align: center;
    color: #fff;
    font-size: 1.4rem;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 0;
    padding-top: 30px;
    position: relative;
    z-index: 1;
  }

  .history {
    max-width: 400px;
    margin: 20px auto;
    padding: 14px 16px;
    border: 2px solid #ccc;
    border-radius: 10px;
    background: #fff;
    color: #222;
    text-align: left;
    font-size: 18px;
    overflow-y: auto;
    max-height: 200px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.08);
  }

  .history h3 {
    margin: 0 0 10px 0;
    text-align: center;
    font-size: 1.4rem !important;
    font-weight: 600;
    color: #444;
    border-bottom: 1px solid #eee;
    padding-bottom: 6px;
  }

  .history ul {
    margin: 0;
    padding: 0 0 0 18px;
  }

  .history li {
    padding: 3px 0;
    border-bottom: 1px solid #f0f0f0;
    color: #333;
    font-size: 1.1rem !important;
  }

  .history li:last-child {
    border-bottom: none;
  }
</style>

<div id="animation">
  <p class="calculator-title">Calculator with History</p>
  <div class="calculator-container">
      <div class="calculator-output" id="output">0</div>

      <div class="calculator-number">1</div>
      <div class="calculator-number">2</div>
      <div class="calculator-number">3</div>
      <div class="calculator-operation">+</div>

      <div class="calculator-number">4</div>
      <div class="calculator-number">5</div>
      <div class="calculator-number">6</div>
      <div class="calculator-operation">-</div>

      <div class="calculator-number">7</div>
      <div class="calculator-number">8</div>
      <div class="calculator-number">9</div>
      <div class="calculator-operation">*</div>

      <div class="calculator-clear">A/C</div>
      <div class="calculator-number">0</div>
      <div class="calculator-number">.</div>
      <div class="calculator-equals">=</div>

      <div class="calculator-operation">/</div>
      <div class="calculator-operation">//</div>
      <div class="calculator-operation">^</div>
      <div class="calculator-operation">√</div>

      <div class="calculator-analyze" onclick="analyzeHistory('average')">Average</div>
      <div class="calculator-analyze" onclick="analyzeHistory('max')">Max</div>
      <div class="calculator-clear calculator-clear-history" onclick="clearHistory()">Clear History</div>
  </div>
</div>

<div class="history" id="history">
  <h3>History</h3>
  <ul id="history-list"></ul>
</div>

<script>
let firstNumber = null;
let operator = null;
let nextReady = true;
let justCalculated = false;
let historyArray = [];

const output = document.getElementById("output");
const numbers = document.querySelectorAll(".calculator-number");
const operations = document.querySelectorAll(".calculator-operation");
const clear = document.querySelectorAll(".calculator-clear");
const equals = document.querySelectorAll(".calculator-equals");
const historyList = document.getElementById("history-list");

numbers.forEach(button => {
  button.addEventListener("click", function() {
    inputNumber(button.textContent);
  });
});

function inputNumber(value) {
  if (nextReady || justCalculated) {
    output.innerHTML = value;
    nextReady = false;
    if (justCalculated) {
      firstNumber = null;
      operator = null;
      justCalculated = false;
    }
  } else {
    output.innerHTML += value;
  }
}

operations.forEach(button => {
  button.addEventListener("click", function() {
    handleOperation(button.textContent);
  });
});

function handleOperation(choice) {
  if (choice === "√") {
    let val = parseFloat(output.innerHTML);
    let sqrtResult = parseFloat(Math.sqrt(val).toFixed(10));
    output.innerHTML = sqrtResult.toString();
    let expr = `√${val} = ${sqrtResult}`;
    addHistory(expr);
    historyArray.push({ expression: expr, result: sqrtResult });
    nextReady = true;
    justCalculated = true;
    return;
  }
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
  result = parseFloat(result.toFixed(10));
  let expr = `${first} ${operator} ${second} = ${result}`;
  addHistory(expr);
  historyArray.push({ expression: expr, result: result });
  return result;
}

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

clear.forEach(button => {
  button.addEventListener("click", function() {
    clearCalc();
  });
});

function clearCalc() {
  firstNumber = null;
  operator = null;
  nextReady = true;
  justCalculated = false;
  output.innerHTML = "0";
}

function addHistory(entry) {
  let li = document.createElement("li");
  li.textContent = entry;
  historyList.appendChild(li);
}

function clearHistory() {
  historyArray = [];
  historyList.innerHTML = "";
}

function analyzeHistory(stat) {
  if (historyArray.length === 0) {
    output.innerHTML = "No history";
    return;
  }
  let value = 0;
  if (stat === "average") {
    let sum = 0;
    for (let i = 0; i < historyArray.length; i++) {
      sum += historyArray[i].result;
    }
    value = parseFloat((sum / historyArray.length).toFixed(10));
  } else if (stat === "max") {
    value = historyArray[0].result;
    for (let i = 1; i < historyArray.length; i++) {
      if (historyArray[i].result > value) {
        value = historyArray[i].result;
      }
    }
  }
  output.innerHTML = value;
}