div
<template>
  <div>
    <div class="expenses">
      <div class="balance">
        <span>Balance</span>
        <p>{{ allExpenses.balance }}$</p>
      </div>
      <div class="income">
        <span>Income</span>
        <p>{{ allExpenses.income }}$</p>
      </div>
      <div class="expense">
        <span>Expense</span>
        <p>{{ allExpenses.expense }}$</p>
      </div>
    </div>

    <div
      class="history"
      v-for="history in allExpenses.history"
      :key="history.title"
      :class="[history.number > 0 ? 'border-green' : 'border-red']"
    >
      <div class="history__date">{{ history.date }}</div>
      <div class="history__title">{{ history.title }}</div>
      <div class="history__number">{{ history.number }}$</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Expenses',

  props: {
    allExpenses: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style scoped>
.expenses {
  width: 800px;
  margin: 70px auto;
  display: flex;
  justify-content: space-between;
}

.balance {
  background: #ffff;
  padding: 20px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  width: 200px;
  height: 150px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  border-bottom: 4px solid orange;
}

.balance span {
  position: absolute;
  top: 0;
  left: 0;
  background: orange;
  color: #fff;
  font-size: 12px;
  padding: 5px;
}

.income {
  background: #ffff;
  padding: 20px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  width: 200px;
  height: 150px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  border-bottom: 4px solid #42b983;
}

.income span {
  position: absolute;
  top: 0;
  left: 0;
  background: #42b983;
  color: #fff;
  font-size: 12px;
  padding: 5px;
}

.expense {
  background: #ffff;
  padding: 20px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  width: 200px;
  height: 150px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  border-bottom: 4px solid red;
}

.expense span {
  position: absolute;
  top: 0;
  left: 0;
  background: red;
  color: #fff;
  font-size: 12px;
  padding: 5px;
}

p {
  font-size: 20px;
}

.history {
  width: 800px;
  margin: 15px auto;
  background: #fff;
  padding: 12px;
  display: flex;
  justify-content: space-between;
  animation: animate 0.5s linear;
}

@keyframes animate {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.border-green {
  border-left: 3px solid #42b983;
}

.border-red {
  border-left: 3px solid red;
}
</style>
