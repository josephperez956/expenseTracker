<script setup>
     import Header from './components/Header.vue';
     import Balance from './components/Balance.vue';
     import IncomeExpenses from './components/IncomeExpenses.vue';
     import {ref, computed} from 'vue'

     const transactions = ref([
          {id: 1, text: 'Paycheck', amount: 699.99},
          {id: 2, text: 'Food', amount: -20},
          {id: 3, text: 'Bills', amount: -200},
          {id: 4, text: 'Video Games', amount: -54.11},
          {id: 5, text: 'Tax Return', amount: 3000},
     ])

     //get the total
     const total = computed(() => {
          return transactions.value.reduce((acc, transaction) => {
               return acc + transaction.amount
          }, 0)
     })

     // get the income by adding all positive values
     const income = computed(()=>{
          return transactions.value
          .filter((transaction)=> transaction.amount>0)
          .reduce((acc, transaction)=>{
               return acc + transaction.amount
          }, 0)
     })

     // get the expenses by adding all negative values
     const expense = computed(()=>{
          return transactions.value
          .filter((transaction)=> transaction.amount<0)
          .reduce((acc, transaction)=>{
               return acc + transaction.amount
          }, 0)
     })
</script>

<template>
     <Header></Header>
     <div class="container">
          <Balance :total="total"></Balance>
          <IncomeExpenses :income="income" :expense="expense"></IncomeExpenses>
     </div>
</template>