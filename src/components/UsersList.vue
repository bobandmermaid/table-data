<template>
  <el-table
    :data='tableData'
    :tree-props='{children: "children", hasChildren: "hasChildren"}'
    style='width: 100%;'
    row-key="id"
    border
    default-expand-all>
    <el-table-column
      prop='name'
      label='Имя'
      sortable>
    </el-table-column>
    <el-table-column
      prop='phone'
      label='Телефон'
      width='250px'
      sortable>
    </el-table-column>
  </el-table>
</template>

<script>
export default {
  name: 'UsersList',
  props: {
    tableData: {
      type: Array,
      default: () => {},
    },
  },
};
</script>

<style scoped>

</style>
