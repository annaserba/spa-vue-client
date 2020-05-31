<template>
  <Row type="flex" justify="center">
    <Col :xs="{ span: 24 }" :md="{ span: 12 }">
      <Button to="/add">Add</Button>
      <Button v-show="selectId" :to="'/edit' + selectId">Edit</Button>
      <Button v-show="selectId" :to="'/delete' + selectId">Delete</Button>
      <Users :loading="loading" :users="users" />
    </Col>
  </Row>
</template>

<script>
import axios from 'axios'
import { mapGetters } from 'vuex'
import Users from '~/components/User/users.vue'
export default {
  components: {
    Users
  },
  data() {
    return {
      users: [],
      departments: [],
      USER_URL: process.env.USER_URL,
      DEPARTMENT_URL: process.env.DEPARTMENT_URL,
      loading: true
    }
  },
  computed: {
    selectId: mapGetters(['user.vue/getSelectId'])['user.vue/getSelectId']
  },
  mounted() {
    Promise.all([
      axios.get(this.USER_URL + '/api/users'),
      axios.get(this.DEPARTMENT_URL + '/api/departments')
    ]).then(([users, departments]) => {
      const that = this
      this.departments = departments.data
      this.users = users.data.map(({ departmentId, ...user }) => {
        const department = that.departments.filter(
          (depart) => depart.id === departmentId
        )[0]
        return { ...user, departmentTitle: department ? department.title : '' }
      })
      this.loading = false
    })
  }
}
</script>
