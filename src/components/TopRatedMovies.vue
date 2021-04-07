<template>
  <div class="container">
    <div class="title">Top Rated Movies</div>
    <div class="card-wrapper">
      <div v-for="movies in topRatedMovies" :key="movies.id" class="card">
        <div style="font-size:22px;margin-bottom:10px">{{ movies.title }}</div>

        <img :src="path + movies.poster_path" />
        <div style="margin-top:10px">
          <span style="font-size:20px;">Rated:</span>{{ movies.vote_average }}
        </div>
        <div style="font-size:18px">
          <strong>Release Date:</strong>{{ movies.release_date }}
        </div>
      </div>
    </div>
    <paginate
      :page-count="total_pages"
      :page-range="2"
      :click-handler="clickCallback"
      :prev-text="'Prev'"
      :next-text="'Next'"
      :container-class="'pagination'"
      :page-class="'page-item'"
    >
    </paginate>
  </div>
</template>
<script>
import axios from "axios";
import Paginate from "vuejs-paginate";

export default {
  name: "TopRatedMovies",
  components: {
    Paginate,
  },
  data() {
    return {
      topRatedMovies: [],
      path: "https://www.themoviedb.org/t/p/w220_and_h330_face",
      total_pages: 0,
    };
  },
  mounted() {
    this.getTopRetedMovies();
  },
  methods: {
    getTopRetedMovies() {
      let params = { page: this.current_page, language: this.language };
      axios
        .get(
          "https://api.themoviedb.org/3/movie/top_rated?api_key=38e9b0e2ec78d2cc9ffdf8c731323f89",
          {
            params: params,
          }
        )
        .then((response) => {
          this.topRatedMovies = response.data.results;
          this.total_pages = response.data.total_pages;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    clickCallback(page) {
      this.current_page = page;
      this.getTopRetedMovies();
    },
  },
};
</script>
<style>
.card-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
.card {
  max-width: 220px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  text-align: center;
  position: relative;
  box-shadow: 0 3px 1px -2px rgb(0 0 0 / 20%), 0 2px 2px 0 rgb(0 0 0 / 14%),
    0 1px 5px 0 rgb(0 0 0 / 12%);
  margin: 1.5rem 0;
  padding: 1rem;
}

ul.pagination {
  color: black;
  float: right;
  text-align: center;
  padding: 20px 0;
  list-style: none;
  position: relative;
  z-index: 6;
  margin: 50px 0;
}
li {
  text-decoration: none;
  display: inline-block;
  text-transform: uppercase;
  margin: 0 3px 6px;
  min-width: 38px;
  height: 38px;
  min-width: 38px;
  line-height: 38px;
  padding: 0;
  font-weight: 700;
  border-radius: 38px;
  border: 2px solid red;
  background: #171a29;
  color: red;
}
li:first-child,
li:last-child {
  padding: 0 16px;
  margin: 0 12px 6px;
}
</style>
