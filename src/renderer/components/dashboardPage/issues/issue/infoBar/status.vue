<template>
  <el-tag
    size="mini"
    :type="tagType"
    class="text-uppercase status"
  >
    {{ status.name }}
  </el-tag>
</template>

<script>
export default {
  props: {
    status: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    tagType () {
      const statusName = this.status.name.toLowerCase()
      const statusTypeMap = {
        'done': 'success',
        'selected to development': 'info',
        'to do': 'info',
        'in progress': 'warning'
      }

      return statusTypeMap[statusName] || 'danger'
    }
  }
}
</script>

<style lang="scss" scoped>
  .status {
    font-weight: 700;
  }
</style>
