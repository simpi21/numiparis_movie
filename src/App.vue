<template>
  <div id="app">
    <upcoming-movies></upcoming-movies>
    <top-rated-movies></top-rated-movies>
  </div>
</template>

<script>
import TopRatedMovies from "./components/TopRatedMovies.vue";
import UpcomingMovies from "./components/UpcomingMovies.vue";

export default {
  components: { TopRatedMovies, UpcomingMovies },
  name: "App",
};
</script>

<style>
body {
  margin: 0;
}

.container {
  margin-left: auto;
  margin-right: auto;
  position: relative;
}

@media screen and (max-width: 576px) {
  .container {
    padding-left: 1rem;
    padding-right: 1rem;
  }
}

@media screen and (min-width: 576px) {
  .container {
    width: 540px;
    max-width: 100%;
  }
}

@media screen and (min-width: 768px) {
  .container {
    width: 720px;
    max-width: 100%;
  }
}

@media screen and (min-width: 992px) {
  .container {
    width: 900px;
    max-width: 100%;
  }
}

@media screen and (min-width: 1200px) {
  .container {
    width: 1120px;
    max-width: 100%;
  }
}
</style>
