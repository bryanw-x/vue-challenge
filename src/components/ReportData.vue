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
  </tr>
</template>

<script>

export default {
  props: {
    report: {
      type: Object,
      required: true,
    }
  }
};
</script>
