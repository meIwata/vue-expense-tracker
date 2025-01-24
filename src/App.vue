<template>
    <Header />
    <div class="container">
        <Balance :total="+total" />
        <IncomeExpenses :income="+income" :expenses="-expenses" />
        <TransactionList :transactions="transactions" />
        <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { useToast } from 'vue-toastification';

import { ref, computed } from 'vue';

const toast = useToast();

const transactions = ref([
    { id: 1, text: 'Flower', amount: -19.99 },
    { id: 2, text: 'Salary', amount: 300 },
    { id: 3, text: 'Book', amount: -27.99 },
    { id: 2, text: 'Cash dividend', amount: 90 },
]);

// 取得總額
const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
        return acc + transaction.amount;
    }, 0).toFixed(2); // .toFixed(2)到小數後兩位
});

// 取得收入
const income = computed(() => {
    return transactions.value
        .filter((transaction) => transaction.amount > 0)
        .reduce((acc, transaction) => acc + transaction.amount, 0)
        .toFixed(2);
});

// 取得支出
const expenses = computed(() => {
    return transactions.value
        .filter((transaction) => transaction.amount < 0)
        .reduce((acc, transaction) => acc + transaction.amount, 0)
        .toFixed(2);
});

// 增加交易
const handleTransactionSubmitted = (transactionData)=>{
    // console.log(transactionData);
    transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  });

    // console.log(generateUniqueId());
    toast.success('Transaction added.');
}

// 產生 unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

</script>