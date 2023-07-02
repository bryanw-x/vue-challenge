<template>
  <tr>
    <td>{{ report.school }}</td>
    <td>{{ report.division }}</td>
    <td>{{ report.conference }}</td>
    <td>{{ report.ranking }}</td>
    <td>{{ report.gpa.min }}</td>
    <td>{{ report.gpa['25%'] }}</td>
    <td>{{ report.gpa['50%'] }}</td>
    <td>{{ report.gpa['75%'] }}</td>
    <td>{{ report.gpa.max }}</td>
    <td>{{ report.sat.reading.min }}</td>
    <td>{{ report.sat.reading.max }}</td>
    <td>{{ report.sat.math.min }}</td>
    <td>{{ report.sat.math.max }}</td>
    <td>{{ report.act.min }}</td>
    <td>{{ report.act.max }}</td>
    <td>{{ getSatReadScore }}</td>
    <td>{{ getSatMathScore }}</td>
    <td>{{ getActScore }}</td>
  </tr>
</template>

<script>

export default {
  props: {
    report: {
      type: Object,
      required: true,
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
    }
  }
};
</script>
