<template>
    <Header></Header>
    <div class="container">
            <Balance :total= "total"></Balance>
            <IncomeExpenses :expenses="+expenses" :income="+income"></IncomeExpenses>
            <TransactionList :transactions = "transactions"></TransactionList>
            <AddTransaction @transactionSubmit="transactionHandler"></AddTransaction>
    </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';
import { ref, computed } from 'vue';
import {useToast} from 'vue-toastification';

const toast = useToast();

const transactions = ref([]);

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

//Adds transactions
const transactionHandler = (transactionInfo) => {
    transactions.value.push({
        id: idMaker(),
        text: transactionInfo.text,
        amount: transactionInfo.amount,
    });
    toast.success('Transaction added!')
};

//Id Maker
const idMaker = () => {
    return transactions.value.length + 1;
}

</script>
