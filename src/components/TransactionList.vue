<template>
    <h3>History</h3>
        <ul id="list" class="list">
            <li v-for="transaction in transactions" :key="transactions.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
               {{transaction.text}} <span>£{{transaction.amount}}</span>
                <button class="delete-btn">x</button>
            </li>
        </ul>
</template>

<script setup>
    const transactions=
    [{id:1, text: "Salary", amount: 300},
    {id:2, text: "Date", amount: -100}
    ];
</script>