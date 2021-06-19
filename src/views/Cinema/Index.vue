<template>
  <div class="content">
    <section class="line" v-for="genre in genres" :key="genre.id">
      <h2>{{ genre.name }}</h2>
      <div class="line_card_group">
        <div v-for="movie in genre.movies" :key="movie.id">
          <vs-card v-if="movie.poster_path !== null" class="line_card">
            <template #img>
              <img
                :src="`https://www.themoviedb.org/t/p/w600_and_h900_bestv2/${movie.poster_path}`"
                alt=""
              />
            </template>
            <template #text>
              <p style="display: none">
                Lorem ipsum dolor sit amet consectetur, adipisicing elit.
              </p>
              <p>Жанр: {{ movie.genre_ids.join(" ") }}</p>
              <!-- <p>Альбом: {{ release.collectionName }}</p> -->
            </template>
            <template #title>
              <h3>{{ movie.original_title }}</h3>
            </template>
            <!-- <template #buttons>
           
          </template> -->
            <template #interactions>
              <vs-button danger icon>
                {{ movie.vote_average }}
              </vs-button>
              <vs-button class="btn-chat" shadow primary>
                <span class="span">{{ fmtDate(movie.release_date) }}</span>
              </vs-button>
            </template>
          </vs-card>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
const API_KEY = "52217232f795bbefbb1b7c951aae98ad";

export default {
  name: "Cinema",
  data() {
    return {
      genres: [],
      movies: [],
    };
  },
  methods: {
    fmtDate(d) {
      let c = new Date(d);
      return `${c.getDate()}/${c.getMonth() + 1}/${c.getFullYear()}`;
    },
  },
  created() {
    axios
      .get(
        `https://api.themoviedb.org/3/genre/movie/list?api_key=${API_KEY}&language=en-US`
      )
      .then((r) => {
        r.data.genres.map((g) => {
          axios
            .get(
              `https://api.themoviedb.org/3/discover/movie?with_genres=${g.id}&sort_by=release_date.desc&api_key=${API_KEY}`
            )
            .then((x) => {
              g.movies = x.data.results;
              this.genres.push(g);
            });
        });
      });
  },
};
</script>

<style lang="stylus">
h2 {
  text-align: left;
}

.line_card_group {
  display: flex;
  min-width: 100vw;
  padding: 2em;
  overflow-y: auto;
}

.line_card {
  display: inline-block;
  width: fit-content;
  min-width: 330px;
  margin: 0 1em;
  text-align: left;
}

.line {
  min-width: 100vw;
  min-height: 10em;
  position: relative;
}
</style>
