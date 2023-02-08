<template>
  <navbar
    @modalExpenseShow="modalExpenseToggle"
    @modalIncomeShow="modalIncomeToggle"
  />
  <income-modal
    @modalIncomeToggle="modalIncomeToggle"
    :status="modalIncomeStatus"
    @storeExpense="storeExpense"
  />
  <expense-modal
    @modalExpenseToggle="modalExpenseToggle"
    :status="modalExpenseStatus"
    @storeExpense="storeExpense"
  />
  <expenses :allExpenses="expenses" />
</template>

<script>
import Navbar from './components/NavbarComponent.vue'
import IncomeModal from './components/IncomeModal.vue'
import ExpenseModal from './components/ExpenseModal.vue'
import Expenses from './components/ExpensesComponent.vue'

export default {
  name: 'App',
  components: {
    Navbar,
    IncomeModal,
    ExpenseModal,
    Expenses,
  },

  data() {
    return {
      modalIncomeStatus: false,
      modalExpenseStatus: false,
      expenses: {
        balance: 0,
        income: 0,
        expense: 0,
        history: [],
      },
    }
  },
  methods: {
    modalExpenseToggle() {
      this.modalExpenseStatus = !this.modalExpenseStatus
    },

    modalIncomeToggle() {
      this.modalIncomeStatus = !this.modalIncomeStatus
    },

    storeExpense(payload) {
      const number = parseInt(payload.number)
      if (number > 1) {
        this.expenses = {
          ...this.expenses,
          income: this.expenses.income + number,
          balance: this.expenses.balance + number,
          history: [
            { title: payload.title, number: number, date: payload.date },
            ...this.expenses.history,
          ],
        }
      } else if (number < 1) {
        this.expenses = {
          ...this.expenses,
          expense: this.expenses.expense + number,
          balance: this.expenses.balance + number,
          history: [
            { title: payload.title, number: number, date: payload.date },
            ...this.expenses.history,
          ],
        }
      }
      this.modalExpenseStatus = false
      this.modalIncomeStatus = false
    },
  },

  mounted() {
    const expensesFromLocalStorage = localStorage.getItem('expenses')
    if (expensesFromLocalStorage) {
      this.expenses = JSON.parse(expensesFromLocalStorage)
    }
  },

  watch: {
    expenses: {
      handler(newExpenses) {
        localStorage.setItem('expenses', JSON.stringify(newExpenses))
      },
      deep: true,
    },
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: #fafafa;
  font-family: sans-serif;
}
</style>
