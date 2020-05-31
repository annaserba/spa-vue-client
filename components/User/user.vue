<template>
  <Form
    :model="user"
    :rules="rules"
    :style="{ 'max-width': '300px', 'margin-top': '20px' }"
  >
    <FormItem prop="userName">
      <Input v-model="user.userName" type="text" placeholder="Username">
        <Icon slot="prepend" type="ios-person-outline"></Icon>
      </Input>
    </FormItem>
    <FormItem prop="userName">
      <Select v-model="user.departmentId">
        <Option
          v-for="department in departments"
          :key="department.id"
          :value="department.id"
          >{{ department.title }}</Option
        >
      </Select>
    </FormItem>
    <FormItem>
      <Button type="primary" @click="handleSubmit">Save</Button>
      <Button to="/">Back</Button>
    </FormItem>
  </Form>
</template>
<script>
import axios from 'axios'
import { mapActions } from 'vuex'
export default {
  props: {
    departments: {
      type: Array,
      default() {
        return []
      }
    },
    user: {
      type: Object,
      default() {
        return { id: 0, userName: '', departmentId: 0 }
      }
    }
  },
  data() {
    return {
      USER_URL: process.env.USER_URL,
      rules: {
        userName: [
          {
            required: true,
            message: 'Please fill in the user name',
            trigger: 'blur'
          }
        ],
        departmentId: [
          {
            required: true,
            message: 'Please fill in the user name',
            trigger: 'blur'
          }
        ]
      }
    }
  },
  methods: {
    ...mapActions(['user.vue/setSelect']),
    handleSubmit(context) {
      const that = this
      if (!this.user.id) {
        axios
          .post(this.USER_URL + '/api/users', this.user)
          .then(function(response) {
            that.successSave(that, response)
          })
      } else {
        axios
          .put(this.USER_URL + '/api/users/' + this.user.id, this.user)
          .then(function(response) {
            that.successSave(that, response)
          })
      }
    },
    successSave(context, response) {
      context['user.vue/setSelect'](null)
      context.$router.back()
    }
  }
}
</script>
