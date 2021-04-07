<template>
  <div class="">
    <div class="container"><div class="title">Upcoming Movies</div></div>
    <carousel
      :paginationEnabled="true"
      :per-page="5"
      :paginationSize="total_pages"
      :autoplay="true"
      :navigationEnabled="true"
      :pagination-click="handleClick"
      navigationNextLabel="▶ Next"
    >
      <slide v-for="movies in upcomingMovies" :key="movies.id">
        <div class="img-container">
          <img :src="path + movies.poster_path" />
          <div class="text">
            <span style="font-size:18px;margin-right:10px">Realese Date:</span
            >{{ movies.release_date }}
          </div>
        </div>
      </slide>
    </carousel>
  </div>
</template>
<script>
import axios from "axios";
import { Carousel, Slide } from "vue-carousel";
export default {
  name: "UpcomingMovies",
  components: {
    Carousel,
    Slide,
  },
  data() {
    return {
      total_pages :0,
      isSelected: true,
      upcomingMovies: [],
      path: "https://www.themoviedb.org/t/p/w220_and_h330_face",
    };
  },
  mounted() {
    this.getUpcomingMovies();
  },
  methods: {
    getUpcomingMovies() {
      let params = { page: this.current_page, language: this.language };
      axios
        .get(
          "https://api.themoviedb.org/3/movie/upcoming?api_key=38e9b0e2ec78d2cc9ffdf8c731323f89",
          {
            params: params,
          }
        )
        .then((response) => {
          this.upcomingMovies = response.data.results;
          this.total_pages = response.data.total_pages;
          console.log(response.data);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    handleClick(page) {
      this.current_page = page;
      this.getTopRetedMovies();
    },
  },
};
</script>
<style>
.title {
  font-size: 32px;
  margin-bottom: 20px;
  margin-top: 50px;
}

.VueCarousel-wrapper {
  background: #171a29;
}
.VueCarousel-dot[data-v-438fd353] {
  display: none !important;
}
.VueCarousel-navigation-button[data-v-453ad8cd] {
  top: 106% !important;
  right: 100px;
  color: #171a29;
  background: red;
  width: 80px;
}
.img-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 1rem;
}
.text {
  margin-top: 10px;
  color: #fff;
}
</style>
