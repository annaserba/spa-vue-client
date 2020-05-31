<template>
  <Row type="flex" justify="center">
    <Col><User :departments="departments" :user="user" /> </Col>
  </Row>
</template>
<script>
import axios from 'axios'
import User from '~/components/User/user.vue'
export default {
  components: {
    User
  },
  asyncData({ app, env, route }) {
    return Promise.all([
      axios.get(env.USER_URL + '/api/users/' + route.params.id),
      axios.get(env.DEPARTMENT_URL + '/api/departments')
    ]).then(([user, departments]) => {
      return {
        departments: departments.data,
        user: user.data
      }
    })
  }
}
</script>
