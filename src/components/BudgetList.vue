<template>
  <div class="budget-list-wrap">
    <div class='buttons-wrap'>
      <el-button @click='filterBudgetList("OUTCOME")' type="danger" size="mini">Show outcomes</el-button>
      <el-button @click='filterBudgetList("INCOME")' type="success" size="mini">Show incomes</el-button>
      <el-button @click='filterBudgetList("ALL")'  type="primary" size="mini">Show all</el-button>
    </div>

    <el-card :header="header">
      <template v-if="!isEmpty">
        <BudgetListItem @deleteBudgetListItem='deleteItem' :list="list" :filter="filter"/>
      </template>
      <el-alert v-else :title="emptyTitle" type="info" :closable="false"
      ></el-alert>
    </el-card>
  </div>
</template>

<script>
import BudgetListItem from '@/components/BudgetListItem';

export default {
  name: 'BudgetList',
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    header: 'Budget List',
    emptyTitle: 'Empty List',
    filter: {
      'outcome': true,
      'income': true
    }
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    },
  },
  created() {
      this.filterBudgetList('ALL');
  },
  components: {
    BudgetListItem
  },
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id);
    },
    filterBudgetList(type) {
      if (type === 'OUTCOME') {
        this.filter.outcome = true;
        this.filter.income = false;
      } else if (type === 'INCOME') {
        this.filter.outcome = false;
        this.filter.income = true;
      } else {
        this.filter.outcome = true;
        this.filter.income = true;
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .budget-list-wrap {
    max-width: 500px;
    margin: auto;
    text-align: center;
  }

  .buttons-wrap {
    max-width: 500px;
    display: flex;
    align-items: center;
    justify-content: space-around;
    padding: 0 0 20px;
  }

</style>
