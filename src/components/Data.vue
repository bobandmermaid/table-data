<template>
  <div class='table'>
    <user-popup
      :tableData = 'tableData'
      @addUser = 'saveUser($event)'
    />
    <users-list
      :tableData = 'tableDataChildren'
    />
  </div>
</template>

<script>
import UserPopup from './UserPopup';
import UsersList from './UsersList';

export default {
  name: 'Data',
  components: {
    'users-list': UsersList,
    'user-popup': UserPopup
  },
  data() {
    return {
      tableData: []
    };
  },
  created() {
    this.getList();
  },
  methods: {
    saveUser(data) {
      const chief = this.tableData.find(user => user.id === data.chiefId);
      const result = {
        id: this.tableData.length + 1,
        name: data.name,
        phone: data.phone,
        parentId: chief ? chief.id : null,
        level: chief ? chief.level + 1 : 1
      };

      this.tableData.push(result);
      localStorage.setItem('tableData', JSON.stringify(this.tableData));
    },
    getList() {
      this.tableData = JSON.parse(localStorage.getItem('tableData')) || [];
    },
  },
  computed: {
    tableDataChildren() {
      const tableData = this.tableData
        .map((elem) => Object.assign(elem, { children: [] }))
        .sort((a, b) => (a.level < b.level ? 1 : -1));

      const res = tableData.slice();

      tableData.forEach((user) => {
        res.forEach((item) => {
          if (user.parentId === item.id) {
            item.children.push(user);
          }
        });
      });

      return res.filter((node) => node.level === 1);
    }
  }
};
</script>

<style scoped>
.table {
  margin: 150px auto;
  width: 400px;
}
</style>
