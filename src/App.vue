<template>
    <Header></Header>
    <div class="container">
            <Balance :total= "total"></Balance>
            <IncomeExpenses :expenses="+expenses" :income="+income"></IncomeExpenses>
            <TransactionList :transactions = "transactions"></TransactionList>
            <AddTransaction></AddTransaction>
    </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed } from 'vue';


const transactions = ref([
    {id:1, text: "Salary", amount: 300},
    {id:2, text: "Date", amount: -100}
    ]);

// Balance
const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
        return acc + transaction.amount;
    }, 0);
});

//Income
const income = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
        return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

//Expenses
const expenses = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
        return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});
</script>
