<template>
  <Table border :columns="columns" :data="users" :loading="loading"></Table>
</template>
<script>
export default {
  props: {
    loading: Boolean,
    users: {
      type: Array,
      default: null
    },
    columns: {
      type: Array,
      default() {
        return [
          {
            title: '#',
            key: 'id',
            sortable: true
          },
          {
            title: 'Username',
            key: 'userName'
          },
          {
            title: 'Department',
            key: 'departmentTitle'
          }
        ]
      }
    }
  }
}
</script>
