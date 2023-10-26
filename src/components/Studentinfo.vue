<template>
  <div class="student-profile">
    <div class="student-info">
      <h2>{{ student.name }}</h2>
      <img :src="student.photo" :alt="student.name" class="student-photo">
    </div>
    <div class="student-details">
      <p><strong>Група:</strong> {{ student.group }}</p>
      <p><strong>Оцінка:</strong> {{ student.mark }}</p>
      <p><strong>Практика:</strong> {{ student.isDonePr ? 'Завершена' : 'Не завершена' }}</p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
const API_URL = "http://34.82.81.113:3000"; 
export default {
  props: {
    id: {
      type: String, 
      required: true 
    },
  },
  data() {
    return {
      student: {},
      loading: true, 
    };
  },
  mounted() {
    axios.get(`${API_URL}/students/${this.id}`)
      .then((response) => {
        this.student = response.data;
        this.loading = false; 
      })
      .catch((error) => {
        console.error("Ошибка при загрузке данных студента:", error);
        this.loading = false; 
      });
  }
};
</script>