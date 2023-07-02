<template>
  <tr :class="{ 'light-blue-row': applyBlueRow }">
    <td>{{ report.school }}</td>
    <td>{{ report.division }}</td>
    <td>{{ report.conference }}</td>
    <td>{{ report.ranking }}</td>
    <td>{{ report.gpa.min }}</td>
    <td>{{ report.gpa['25%'] }}</td>
    <GPAColorCode :gpa="report.gpa['50%']" />
    <td>{{ report.gpa['75%']  }}</td>
    <td>{{ report.gpa.max }}</td>
    <td>{{ getSatReadScore }}</td>
    <td>{{ getSatMathScore }}</td>
    <td>{{ getActScore }}</td>
  </tr>
</template>

<script>
import GPAColorCode from './GPAColorCode.vue';

export default {
  name: "ReportData",
  components: {
    GPAColorCode
  },
  props: {
    report: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true
    }
  },
  computed: {
    getSatReadScore() {
      return `${this.report.sat.reading.min} - ${this.report.sat.reading.max}`
    },
    getSatMathScore(){
      return `${this.report.sat.math.min} - ${this.report.sat.math.max}`
    },
    getActScore(){
      return `${this.report.act.min} - ${this.report.act.max}`
    },
    applyBlueRow() {
      return this.index % 2 === 1;
    }
  }
};
</script>
<style scoped>
.light-blue-row {
  background-color: #e6f2ff;
}
</style>
