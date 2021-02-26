<template>
  <div class='buttons-class'>
    <el-button @click='outcomes' plain type="info" size="mini">Show outcomes</el-button>
    <el-button plain type="info" size="mini">Show incomes</el-button>
    <el-button  plain type="info" size="mini">Show all</el-button>
    <el-button plain type="info" size="mini">Sort list</el-button>
  </div>
</template>

<script>
export default {
  name: 'SortBtns',
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  methods: {
    outcomes() {
      this.list
    }
  }
}
</script>

<style scoped>
  .buttons-class {
    display: flex;
    align-items: center;
    justify-content: space-around;
    padding: 20px;
    width: 500px;
    margin: 0 auto;
  }
</style>