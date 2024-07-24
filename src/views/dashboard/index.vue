<template>
  <div class="dashboard-container">
    <adminDashboard />
  </div>
</template>

<script>
import adminDashboard from './admin'

export default {
  name: 'Dashboard',
  components: { adminDashboard }
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>
