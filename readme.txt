Expense Tracker App JavaScript

This document provides an overview of the JavaScript code used in the Expense Tracker App project. The script manages the functionality of adding, removing, and updating transactions in an expense tracker.

Table of Contents

DOM Elements

Local Storage

Functions
Function: addTransaction
Function: generateID
Function: addTransactionDOM
Function: updateValues
Function: removeTransaction
Function: updateLocalStorage
Function: init

Event Listener

DOM Elements

The script references various DOM elements to interact with the HTML document.


const balance = document.getElementById('balance');
const money_plus = document.getElementById('money-plus');
const money_minus = document.getElementById('money-minus');
const list = document.getElementById('list');
const form = document.getElementById('form');
const text = document.getElementById('text');
const amount = document.getElementById('amount');





________________________________________________________________________________________________________________________________________________

Local Storage
The script utilizes local storage to store and retrieve transaction data.


const localStorageTransactions = JSON.parse(localStorage.getItem('transactions'));

let transactions = localStorage.getItem('transactions') !== null ? localStorageTransactions : [];

................................................................................................................................................
Functions


Function: addTransaction
This function handles the addition of a new transaction to the list. It validates the input and updates the DOM and local storage accordingly.


function addTransaction(e) {
  e.preventDefault();

  if (text.value.trim() === '' || amount.value.trim() === '') {
    alert('Please add a text and amount');
  } else {
    const transaction = {
      id: generateID(),
      text: text.value,
      amount: +amount.value
    };

    transactions.push(transaction);

    addTransactionDOM(transaction);

    updateValues();

    updateLocalStorage();

    text.value = '';
    amount.value = '';
  }
}


............................................................................................................................................

Function: generateID
This function generates a random ID for each transaction.


function generateID() {
  return Math.floor(Math.random() * 100000000);
}



.............................................................................................................................................

Function: addTransactionDOM
This function adds the transaction to the DOM by dynamically creating HTML elements.


function addTransactionDOM(transaction) {
  // ... HTML creation based on transaction data ...
}



.............................................................................................................................................

Function: updateValues
This function updates the balance, income, and expense values based on the transactions.


function updateValues() {
  // ... calculation of total, income, and expense ...
}

..............................................................................................................................................

Function: removeTransaction
This function removes a transaction by its ID.


function removeTransaction(id) {
  transactions = transactions.filter(transaction => transaction.id !== id);

  updateLocalStorage();

  init();
}


................................................................................................................................................

Function: updateLocalStorage
This function updates the local storage with the current transactions.


function updateLocalStorage() {
  localStorage.setItem('transactions', JSON.stringify(transactions));
}


................................................................................................................................................

Function: init
This function initializes the app by clearing the transaction list, adding transactions from local storage, and updating values.


function init() {
  list.innerHTML = '';

  transactions.forEach(addTransactionDOM);
  updateValues();
}

init();


................................................................................................................................................
Event Listener
An event listener is attached to the form to handle the submission of new transactions.

form.addEventListener('submit', addTransaction);

................................................................................................................................................