<template>
  <div class="photo-widget">
    <h2>{{ title }}</h2>
    <img :src="photoUrl" :alt="title" />
    <button @click="getRandomPhoto">Lagi ?</button>
    <h4 id="company">&copy; 2023 CompanyDonHan.org</h4>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      photoUrl: '',
    };
  },
  mounted() {
    this.getRandomPhoto();
  },
  methods: {
    async getRandomPhoto() {
      try {
        const apiKey = '38037020-2c48722c03be8437a05b588e6';
        const apiUrl = `https://pixabay.com/api/?key=${apiKey}&q=nature&image_type=photo&orientation=horizontal`;

        const response = await fetch(apiUrl);
        const data = await response.json();

        const randomIndex = Math.floor(Math.random() * data.hits.length);
        const randomPhoto = data.hits[randomIndex];

        this.title = randomPhoto.tags;
        this.photoUrl = randomPhoto.webformatURL;
      } catch (error) {
        console.error('Error fetching random photo:', error);
      }
    },
  },
};
</script>

<style scoped>
.photo-widget {
  border: 1px solid maroon;
  padding: 20px;
  margin-bottom: 20px;
  margin-left: 300px;
  margin-right: 300px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: gray;
}

.photo-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  max-width: 500px;
  margin-top: 10px;
}

.photo-container img {
  max-width: 100%;
  max-height: 100%;
}

.photo-widget button {
  margin-top: 10px;
  padding: 10px;
}

.photo-widget button:hover {
  color: #c7a51d;
  background-color: maroon;
}

h2 {
  color: maroon;
}

#company {
  color: maroon;
  margin-bottom: 20px;
  font-size: 16px;
}

#company:hover {
  color: #c7a51d;
}
</style>
