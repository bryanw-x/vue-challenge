<template>
  <div class="container">
    <div class="header">
      <i class="profile-picture">profile_image</i>
      <h2 class="athlete-name">{{athlete.name}}</h2>
    </div>
    <div class="student-info">
      <div class="data">
        <ul>
          <li>
            <label>Sport:</label>
            {{athlete.sport}}
          </li>
          <li>
            <label>Class:</label>
            {{athlete.grad_year}}
          </li>
          <li>
            <label>Club:</label>
            {{athlete.club.name}}
          </li>
        </ul>
      </div>
      <div class="data">
        <ul>
          <li>
            <label>High School:</label>
            {{athlete.high_school.name}}
          </li>
          <li>
            <label>GPA:</label>
            {{athlete.gpa}}
          </li>
          <li>
            <label>Desired Major:</label>
            {{athlete.major}}
          </li>
        </ul>
      </div>
      <div class="logo-section">
        <div class="logo">
          <img :src="require('@/assets/Asset_1.png')" alt="Logo Image">
        </div>
        <div class="logo-text">
          <p>Academic Fit Report</p>
        </div>
      </div>
    </div>
    <div class="report-header">
      <table>
        <thead>
          <tr>
            <th>School Name</th>
            <th>Athletic Div</th>
            <th>Conference</th>
            <th>Ranking*<br>(DI NCAA)<br>(DII & DIII Hero Sports)</th>
            <th>Min</th>
            <th>25%</th>
            <th>50%</th>
            <th>75%</th>
            <th>Max</th>
            <th>SAT Reading***<br>25%-75%</th>
            <th>SAT Math***<br>25%-75%</th>
            <th>ACT Composite***<br>25%-75%</th>
          </tr>
        </thead>
        <tbody>
          <ReportCard v-for="report in athlete.report" :key="report.school" :report="report"/>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import ReportCard from './ReportCard.vue'
export default {
  name: "AcademicFitReport",
  props: {
    athlete: {
      type: Object,
      required: false
    }
  },
  components: {
    ReportCard
  }
};
</script>
<style scoped>
.container {
  border-top: 4px solid #0099cc;
  font-family: 'Arial', sans-serif;
  padding: 1em;
}
.header {
  align-items: center;
  color: #0099cc;
}
.profile-picture {
  font-size: 18px;
  margin-right: 10px;
}
.logo-section {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
.logo img {
  height: 58px;
  width: auto;
}
.logo-text p {
  text-align: right;
}
.student-info {
  display: flex;
  justify-content: space-between;
  margin-top: 1em;
}
.data {
  flex: 5;
  width: 45%;
}
.data ul {
  list-style: none;
  padding: 0;
}
.data li {
  margin-bottom: 0.5em;
}
.data label {
  font-weight: bold;
}
table {
  width: 100%;
  border-collapse: collapse;
}
th {
  background-color: black;
  color: white;
  text-align: center;
  font-size: 0.8em;
}

</style>
