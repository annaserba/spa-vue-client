<template>
  <Row class="container">
    <Col class="header"> User </Col>
    <Col class="content">
      <Row type="flex" justify="center">
        <Col>
          <User :departments="departments" />
        </Col>
      </Row>
    </Col>
  </Row>
</template>
<script>
import axios from 'axios'
import User from '~/components/User/user.vue'
export default {
  components: {
    User
  },
  asyncData({ app, env }) {
    return axios
      .get(env.DEPARTMENT_URL + '/api/departments')
      .then((departments) => {
        return {
          departments: departments.data
        }
      })
  }
}
</script>
