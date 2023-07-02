<template>
  <div class="container">
    <div class="header"></div>
      <div class="athlete-avatar-name">
        <input
          type="text"
          class="athlete-name"
          v-model="athleteName"
          @blur="updateProfileAvatar"
        >
      </div>
      <div class="athlete-info">
        <div class="avatar-container">
          <img class="profile-picture" v-if="!useProfileAvatar" :src="athlete.profile_image" alt="Profile Picture" />
          <div class="avatar" :style="{backgroundColor: avatarColor}" v-if="useProfileAvatar">
            {{initials}}
          </div>
        </div>
        <div class="sport-column data">
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
        <div class="school-column data">
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
      <div class="table-wrapper">
        <table>
          <thead>
            <tr>
              <th class="school-name">School Name</th>
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
            <ReportData v-for="(report, index) in athlete.report" :key="report.school" :report="report" :index="index"/>
          </tbody>
        </table>
      </div>
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
  components: {
    ReportData
  },
  data() {
    return {
      athleteName: this.athlete.name,
      useProfileAvatar: !this.athlete.profile_image,
    }
  },
  props: {
    athlete: {
      type: Object,
      required: true
    }
  },
  watch: {
    athlete: {
      handler(newValue) {
        this.athleteName = newValue.name;
        this.useProfileAvatar = !newValue.profile_image;
      },
    deep: true,
  },
  athleteName(newName) {
    this.useProfileAvatar = true;
    this.$emit('name-changed', newName);
  }
},
computed: {
  initials() {
    let names = this.athleteName.split(' ');
    return names[0].substring(0, 1).toUpperCase() + names[names.length - 1].substring(0, 1).toUpperCase();
  },
  avatarColor() {
    const colors = ['#f1603c', '#6082fa', '#827cb8', '#0097a4', '#ffe066', '#ffa94d'];
    let lastName = this.athleteName.split(' ').pop();
    let index = lastName.charCodeAt(0) % colors.length;
    return colors[index];
  },
},
  methods: {
    getInitials() {
      let names = this.athleteName.split(' ');
      let initials = names[0].substring(0, 1).toUpperCase() + names[names.length - 1].substring(0, 1).toUpperCase();
      return initials;
    },
    getColor() {
      let colors = ['#f1603c', '#6082fa', '#827cb8', '#0097a4', '#ffe066', '#ffa94d'];
      let lastName = this.athleteName.split(' ').pop();
      let index = lastName.charCodeAt(0) % colors.length;
      return colors[index];
    },
    updateProfileAvatar() {
      this.useProfileAvatar = true;
      this.useProfileAvatar = this.athleteName !== this.athlete.name;
    }
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
.avatar {
  border-radius: 50%;
  width: 120px;
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 2em;
}
.profile-picture {
  border-radius: 50%;
  width: 120px;
  height: 120px;
  object-fit: cover;
  margin-right: 10px;
}
.athlete-name{
  color: #0099cc;
  border: none;
  background-color: transparent;
  outline: none;
  margin-left: 10px;
}
.logo-section {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
.logo img {
  height: 4em;
  width: auto;
}
.logo-text p {
  text-align: right;
}
.athlete-info {
  display: flex;
  flex-direction: row;
  margin-top: 1em;
}
.athlete-name {
  font-size: 20px
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
.table-wrapper {
  overflow-x: auto;
}
th {
  background-color: black;
  color: white;
  text-align: center;
  font-size: 0.8em;
}
th.school-name {
  position: sticky;
  left: 0;
  z-index: 1;
}
.footer {
  border-bottom: 8px solid #0099cc;
  font-size: 0.8em;
  width: 100%;
  position: fixed;
  bottom: 0;
  left: 0;
}
@media (max-width: 600px) {
  .athlete-info {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
  .athlete-name {
    font-size: 18px;
    text-align: center;
  }
  .data {
    width: 100%;
  }
}
</style>
