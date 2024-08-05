<template>
    <Header></Header>
    <div class="container">
            <Balance></Balance>
            <IncomeExpenses></IncomeExpenses>
            <TransactionList :transactions ="transactions"></TransactionList>
            <AddTransaction></AddTransaction>
    </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref } from 'vue';


const transactions = ref([
    {id:1, text: "Salary", amount: 300},
    {id:2, text: "Date", amount: -100}
    ]);

</script>
