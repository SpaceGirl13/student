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
let firstNumber = null; // first number the user typed before hitting an operator
let operator = null;    //operator the user picked (+, -, *, etc.)




// nextReady starts true so the first keypress replaces the default "0" instead of adding onto it
// flips to false once the user starts typing, and back to true after an operator, =, or √




let nextReady = true;
let justCalculated = false; // True after = is pressed
let historyArray = []; // List storing all past calculation and results




// DOM References
const output = document.getElementById("output");
const numbers = document.querySelectorAll(".calculator-number");
const operations = document.querySelectorAll(".calculator-operation");
const clear = document.querySelectorAll(".calculator-clear:not(.calculator-clear-history)");
const equals = document.querySelectorAll(".calculator-equals");
const historyList = document.getElementById("history-list");




// Number Button Listeners
numbers.forEach(button => {
 button.addEventListener("click", function() {
   inputNumber(button.textContent);
 });
});




// called every time the user clicks a number or decimal button
function inputNumber(value) {
 if (nextReady || justCalculated) {
   output.innerHTML = value;
   nextReady = false; // user has started typing expression, so stop replacing and start appending
   if (justCalculated) {
     // if they just hit equals and start typing, reset everything for a new expression
     firstNumber = null;
     operator = null;
     justCalculated = false;
   }
 } else {
   output.innerHTML += value; // user is mid-number
 }
}








// Operation Button Listeners
// attach a click listener to every operator button




operations.forEach(button => {
 button.addEventListener("click", function() {
   handleOperation(button.textContent);
 });
});




// handles what happens when the user clicks an operator button
function handleOperation(choice) {
 if (choice === "√") { // sqrt function only requires one number
   let val = parseFloat(output.innerHTML);
   let sqrtResult = parseFloat(Math.sqrt(val).toFixed(10));
   output.innerHTML = sqrtResult.toString();
   let expr = `√${val} = ${sqrtResult}`;
   addHistory(expr);
   historyArray.push({ expression: expr, result: sqrtResult });
   nextReady = true; // result is shown, so the next keypress should start a new expression
   justCalculated = true;
   return;
 }
 if (firstNumber === null) {
   firstNumber = parseFloat(output.innerHTML); // save whatever the user typed as the first number
 } else if (!nextReady) {
   // the user picked a new operator without hitting = first, so calculate what's on screen before moving on
   firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
   output.innerHTML = firstNumber.toString();
 }
 operator = choice;
 nextReady = true; // operator was clicked, so the next digit should start a new expression
 justCalculated = false;
}




// Calculations
// does the math between two numbers using the stored operator, then saves the result to historyArray
function calculate(first, second) {
 let result = 0;
 switch (operator) {
   case "+": result = first + second; break;
   case "-": result = first - second; break;
   case "*": result = first * second; break;
   case "/": result = first / second; break;
   case "//": result = Math.floor(first / second); break; // floor (integer) division, rounds down
   case "^": result = Math.pow(first, second); break; // exponents
   default: break;
 }
 result = parseFloat(result.toFixed(10)); // clean up floating point errors




 // build the expression string and push it to both the screen list (in history box) and historyArray
 let expr = `${first} ${operator} ${second} = ${result}`;
 addHistory(expr);
 historyArray.push({ expression: expr, result: result });
 return result;
}




// Equals Button Listener
equals.forEach(button => {
 button.addEventListener("click", function() {
   handleEquals();
 });
});




// runs when the user hits = and displays the final answer
// only works if we actually have a first number and an operator to work with
function handleEquals() {
 if (firstNumber !== null && operator !== null) {
   firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
   output.innerHTML = firstNumber.toString();
   nextReady = true; // result is on screen, so the next keypress starts a new expression
   operator = null;
   justCalculated = true;
 }
}




// Clear Button Listener
clear.forEach(button => {
 button.addEventListener("click", function() {
   clearCalc();
 });
});




// resets the display and all state back to the starting point
// does not touch the history — that stays until the user clicks "Clear History"
function clearCalc() {
 firstNumber = null;
 operator = null;
 nextReady = true; // resets nextReady to true so the display starts fresh on the next keypress
 justCalculated = false;
 output.innerHTML = "0";
}




// History Helpers
// creates a new list item and appends it to the history box on screen
function addHistory(entry) {
 let li = document.createElement("li");
 li.textContent = entry;
 historyList.appendChild(li);
}




// clears both the on-screen history list and historyArray so Average/Max have nothing to read
function clearHistory() {
 historyArray = []; // clears the historyArray
 historyList.innerHTML = ""; // clears on-screen history
}




// analyzes all results saved in historyArray
// "average" - finds the mean of all results
// "max" - finds the largest result
function analyzeHistory(stat) {
 if (historyArray.length === 0) {
   // if the user hasn't done any calculations yet, say there's no history
   output.innerHTML = "No history";
   return;
 }
 let value = 0;
 if (stat === "average") {
   let sum = 0;
   for (let i = 0; i < historyArray.length; i++) {
     sum += historyArray[i].result; // add each stored result to the total
   }
   value = parseFloat((sum / historyArray.length).toFixed(10));
 } else if (stat === "max") {
   value = historyArray[0].result; // start by assuming the first result is the biggest
   for (let i = 1; i < historyArray.length; i++) {
     if (historyArray[i].result > value) {
       value = historyArray[i].result; // if bigger value found in historyArray, update max
     }
   }
 }
 output.innerHTML = value; // show the average or max on the calculator display
}

