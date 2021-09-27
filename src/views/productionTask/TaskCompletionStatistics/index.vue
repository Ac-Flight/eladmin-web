<template>
  <div class="app-container">
    <bar-chart />
    <br>
    <pie-chart />
  </div>
</template>

<script>
import BarChart from './BarChart'
import PieChart from './PieChart'

export default {
  name: 'TaskCompletionStatistics',
  components: { BarChart, PieChart }
}
</script>

<style scoped>

</style>
