<template>
  <td :style="{ backgroundColor: gpaColor }">{{ gpa }}</td>
</template>

<script>
export default {
 name: "GPAColorCode",
 props: {
   gpa: {
     type: Number,
     required: true,
   },
 },
 data() {
   return {
     userGpa: 3.8
   };
 },
 computed: {
   gpaColor() {
     const difference = this.gpa - this.userGpa;

     if (difference > 0.1) {
       return "#d7737d";
     } else if (difference > 0 && difference <= 0.1) {
       return "#c194b5";
     } else if (difference === 0) {
       return "#b4a7d6";
     } else if (difference < 0 && difference >= -0.1) {
       return "#a6a8da";
     } else {
       return "#75ace5";
     }
   }
 }
};
</script>
