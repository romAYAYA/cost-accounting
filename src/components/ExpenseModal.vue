<template>
  <div v-if="status">
    <div class="modal" @click.self="toggle">
      <div class="modal__container">
        <div class="modal__form">
          <form @submit.prevent="addExpense">
            <div class="modal__group">
              <h3>How much did you spend this time?</h3>
            </div>
            <div class="modal__group">
              <input
                type="date"
                class="modal__control"
                placeholder="Source of income"
                v-model="date"
              />
            </div>
            <div class="modal__group">
              <input
                type="text"
                class="modal__control"
                placeholder="Category/Comment"
                v-model="title"
              />
            </div>
            <div class="modal__group">
              <input
                type="number"
                class="modal__control"
                placeholder="Expense..."
                v-model="number"
              />
            </div>
            <div class="modal__group">
              <input
                v-if="title && number && date"
                @click="applyMinusSign"
                type="submit"
                value="Add Expense"
                class="btn"
              />
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ExpenseModal',

  props: {
    status: {
      type: Boolean,
      required: true,
    },
  },

  data() {
    return {
      date: '',
      title: '',
      number: '',
    }
  },

  methods: {
    toggle() {
      this.$emit('modalExpenseToggle')
    },

    addExpense() {
      this.$emit('storeExpense', {
        title: this.title,
        number: this.number,
        date: this.date,
      })
      this.title = ''
      this.number = ''
      this.date = ''
    },

    applyMinusSign() {
      this.number *= -1
    },
  },
}
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
}

.modal__container {
  background: #fff;
  width: 450px;
  padding: 20px;
  border-radius: 5px;
}

.modal__group {
  margin: 15px 0;
}

.modal__control {
  border-bottom: 1px solid silver;
  border-left: none;
  border-right: none;
  border-top: none;
  width: 100%;
  padding: 7px 0;
  outline: none;
}

.btn {
  border: none;
  border-radius: 3px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background: red;
  color: #fff;
  padding: 10px 15px;
  cursor: pointer;
  width: 100%;
  outline: none;
}
</style>
