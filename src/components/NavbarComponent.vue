<template>
  <nav>
    <button class="btn btn-green" @click="openModalIncome">Add Income</button>
    <button class="btn btn-red" @click="openModalExpense">Add Expense</button>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',

  methods: {
    openModalIncome() {
      this.$emit('modalIncomeShow')
    },

    openModalExpense() {  
      this.$emit('modalExpenseShow')
    },
  },
}
</script>

<style scoped>
nav {
  width: 100%;
  height: 60px;
  background: #fff;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
  display: flex;
  justify-content: center;
  align-items: center;
}

.btn {
  border: none;
  border-radius: 3px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);

  color: #fff;
  padding: 10px 15px;
  cursor: pointer;
  outline: none;
  margin-right: 5px;
}

.btn-green {
  background: #42b983;
}

.btn-red {
  background: red;
}
</style>
