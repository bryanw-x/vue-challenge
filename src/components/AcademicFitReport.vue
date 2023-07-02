<template>
  <div class="container">
    <div class="header">
      <h1 class="athlete-name">{{athlete.name}}</h1>
    </div>
    <div class="student-info">
      <img class="profile-picture" :src="athlete.profile_image" alt="Profile Picture"/>
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
          <div class="logo-text">
            <p>Academic Fit Report</p>
          </div>
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
          <ReportData v-for="report in athlete.report" :key="report.school" :report="report"/>
        </tbody>
      </table>
      <tfoot>
        <tr>
          <td colspan="12" class="footer">
            <p>Rankings for Division I schools based on NCAA data (www.ncaa.com) and rankings for Division II & III schools are based on data from Hero Sports (www.herosports.com/rankings)<br>
            ** GPA is based on SportsRecruits members who have shown interest in (favorited) the school and have provided their GPA on their profile<br>
            *** SAT and ACT scores based on national data provided by the National Center of Education Statistics - https://nces.ed.gov/ipeds/
          </p>
          </td>
        </tr>
      </tfoot>
    </div>
  </div>
</template>

<script>
import ReportData from './ReportData.vue'
export default {
  name: "AcademicFitReport",
  props: {
    athlete: {
      type: Object,
      required: false
    }
  },
  components: {
    ReportData
  }
};
</script>
<style scoped>
.container {
  border-top: 8px solid #0099cc;
  font-family: 'Arial', sans-serif;
  padding: 1em;
}
.header {
  align-items: center;
  color: #0099cc;
}
.profile-picture {
  border-radius: 50%;
  width: 120px;
  height: 120px;
  object-fit: cover;
  margin-right: 10px;
}
.athlete-name{
  font-size: 20px;
  color: #0099cc;
}
.logo-section {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
.logo img {
  height: 40%;
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
.footer {
  border-bottom: 8px solid #0099cc;
  font-size: 0.8em;
  width: 100%;
  position: fixed;
  bottom: 0;
  left: 0;
}

</style>
