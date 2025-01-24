<template>
    <h3>Add new transaction</h3>
      <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
          <label for="text">Text</label>
          <input type="text" id="text" v-model="text" placeholder="Enter text..." />
        </div>
        <div class="form-control">
          <label for="amount"
            >Amount <br />
            (negative - expense, positive - income)</label
          >
          <input type="text" id="amount" v-model="amount" placeholder="Enter amount..." />
        </div>
        <button class="btn">Add transaction</button>
      </form>
</template>

<script setup>
  import { ref } from 'vue';
  import { useToast } from 'vue-toastification';

  const text = ref('');
  const amount = ref('');
  const toast = useToast();

  const onSubmit = ()=>{
    if (!text.value || !amount.value) {
      toast.error('Both fileds must be filled'); // 如果兩個欄位或只填一個欄位給於警告
      return;
    }
    // console.log('submit');
    console.log(text.value, amount.value); // 測試輸入資料，console.log資料有進去

    text.value = '';
    amount.value = '';
  };
</script>