<template>
  <el-form-item label="Issue type" label-width="100px">
    <el-checkbox-group v-model="issueTypesSelected">
      <el-checkbox v-for="issue in availableIssueTypes" :key="issue" :label="issue"/>
    </el-checkbox-group>
  </el-form-item>
</template>

<script>
import uniq from 'lodash.uniq'
import { mapGetters, mapMutations, mapState } from 'vuex'

export default {
  computed: {
    ...mapState({
      storeIssueTypes: state => state.filters.issueTypes
    }),
    ...mapGetters({
      getIssues: 'issues/getIssues'
    }),
    availableIssueTypes () {
      const types = this.getIssues.map(issue => issue.fields.issuetype.name)
      return uniq(types)
    },
    issueTypesSelected: {
      get () {
        return this.storeIssueTypes
      },
      set (value) {
        this.setIssueTypeFilter(value)
      }
    }
  },
  methods: {
    ...mapMutations({
      setIssueTypeFilter: 'filters/setIssueTypeFilter'
    })
  }
}
</script>
