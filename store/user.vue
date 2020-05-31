<script>
export default {
  state: { select: null },
  getters: {
    getSelectId(state) {
      return state.select ? state.select.id : 0
    }
  },
  mutations: {
    setSelect(state, select) {
      state.select = select
    }
  },
  actions: {
    setSelect(state, select) {
      state.commit('setSelect', select)
    }
  }
}
</script>
