<template>
  <div class="container">
    <section class="line" v-for="genre in genres" :key="genre.id">
      <h2>{{ genre.name }}</h2>
      <div class="line_card_group">
        <div v-for="movie in genre.series" :key="movie.id">
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
              <h3>{{ movie.name }}</h3>
            </template>
            <!-- <template #buttons>
           
          </template> -->
            <template #interactions>
              <vs-button danger icon>
                {{ movie.vote_average }}
              </vs-button>
              <vs-button class="btn-chat" shadow primary>
                <span class="span">{{ fmtDate(movie.first_air_date) }}</span>
              </vs-button>
            </template>
          </vs-card>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  Name: "Series",
  data() {
    return {
      genres: [
        { id: 0, name: "Popular", series: [] },
        { id: 1, name: "Top Rated", series: [] },
      ],
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
        `https://api.themoviedb.org/3/tv/popular?api_key=52217232f795bbefbb1b7c951aae98ad&language=en-US`
      )
      .then((r) => {
        this.genres[0].series = r.data.results;
      });
    axios
      .get(
        `https://api.themoviedb.org/3/tv/top_rated?api_key=52217232f795bbefbb1b7c951aae98ad&language=en-US`
      )
      .then((x) => {
        this.genres[1].series = x.data.results;
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

.vs-card__img {
  max-height: 400px !important;
}

.line {
  min-width: 100vw;
  min-height: 10em;
  position: relative;
}
</style>
