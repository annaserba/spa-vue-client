<template>
  <Row type="flex" justify="center">
    <Col :xs="{ span: 24 }" :md="{ span: 12 }">
      <Button to="/add" :departments="departments">Add </Button>
      <Users :loading="loading" :users="users" />
    </Col>
  </Row>
</template>

<script>
import axios from 'axios'
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
  mounted() {
    Promise.all([
      axios.get(this.USER_URL + '/api/users'),
      axios.get(this.DEPARTMENT_URL + '/api/departments')
    ]).then(([users, departments]) => {
      this.users = users.data.map(({ id, userName, departmentId }) => {
        const departmentName = departments.data.filter(
          (department) => department.id === departmentId
        )
        return { id, userName, departmentName }
      })
      this.departments = departments.data
      this.loading = false
    })
  }
}
</script>
