<template>
  <div id="app">
    <Form @onFormSubmit='onSubmit'/>
    <TotalBalance :style='{"color": color}' :total='totalBalance'/>
    <BudgetList @deleteItem='onDeleteItem' :list="list"/>
  </div>
</template>

<script>
import BudgetList from '@/components/BudgetList';
import TotalBalance from '@/components/TotalBalance';
import Form from '@/components/Form';

export default {
  name: 'app',
  components: {
    BudgetList,
    TotalBalance,
    Form
  },
  data: () => ({
    list: {
      1: {
        id: 1,
        type: 'INCOME',
        value: 100,
        comment: 'Some income'
      },
      2: {
        id: 2,
        type: 'OUTCOME',
        value: -50,
        comment: 'Some outcome'
      }
    },
    dialogVisible: false
  }),
  computed: {
    totalBalance() {
      const total = Object.values(this.list).reduce((acc, item) =>  acc += item.value, 0);
      return total;
    },
    color() {
      const total = this.totalBalance;
      let color = 'black';
      color = total > 0 ? 'green'
        : total === 0 ? 'black'
        : 'red';
      return color;
    }
  },
  methods: {
    onDeleteItem(id) {
      this.$confirm('Do you want do delete this item?', 'Warning', {
          confirmButtonText: 'Yes',
          cancelButtonText: 'No',
          type: 'warning'
        }).then(() => {
          this.$message({
            type: 'success',
            message: 'Delete completed'
          });
          this.$delete(this.list, id);
        }).catch(() => {
          this.$message({
            type: 'info',
            message: 'Delete canceled'
          });
        });
    },
    onSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      if (newObj.type === 'OUTCOME') {
        newObj.value = -Math.abs(newObj.value);
      }
      this.$set(this.list, newObj.id, newObj);
    },

  }
};
</script>

<style>
#app {
}
</style>
