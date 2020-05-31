<template>
  <Table
    border
    highlight-row
    :columns="columns"
    :data="users"
    :loading="loading"
    @on-current-change="onSelect"
  ></Table>
</template>
<script>
import { mapActions } from 'vuex'
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
  },
  methods: {
    ...mapActions(['user.vue/setSelect']),
    onSelect(currentRow, oldCurrentRow) {
      this['user.vue/setSelect'](currentRow)
    }
  }
}
</script>
