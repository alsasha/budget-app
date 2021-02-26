<template>
  <div>
    <div  class="list-item" v-for="(item, prop) in list" :key="prop"
    v-show="item.type ===  'OUTCOME'? filter['outcome']: filter.income">
      <i :class="icon(item.type)"></i>
      <span class="budget-comment">{{ item.comment }}</span>
      <span :style='{"color": color(item.type)}' class="budget-value">{{ item.value }}</span>
      <el-button @click='deleteBudgetListItem(item.id)' type="danger" size="mini" icon="el-icon-delete" circle></el-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BudgetListItem',
  props: {
    list: {
      type: Object,
      default: () => ({})
    },
    filter: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({

  }),
  methods: {
    deleteBudgetListItem(id) {
      this.$emit('deleteBudgetListItem', id);
    },
    icon(type) {
      return type === 'INCOME' ? 'el-icon-top' : 'el-icon-bottom';
    },
    color(type) {
      return type === 'INCOME' ? 'green' : 'red';
    }
  }
}
</script>

<style scoped>
  .list-item {
    display: flex;
    padding: 10px 15px;
    align-items: center;
  }

  .budget-value{
    font-weight: bold;
    margin: 0 20px 0 auto;
  }
</style>