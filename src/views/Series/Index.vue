<template>
  <div class="container">
    <!-- <vs-button shadow @click="activeDialog = !activeDialog">
      Open Dialog
    </vs-button> -->
    <section class="line" v-for="(genre, genreIndex) in genres" :key="genre.id">
      <h2>{{ genre.name }} | {{ genreIndex }}</h2>
      <div class="line_card_group">
        <div v-for="(movie, movieIndex) in genre.series" :key="movie.id">
          <vs-card
            @click="
              dialogs.data[genreIndex][movieIndex][movie.id] =
                !dialogs.data[genreIndex][movieIndex][movie.id]
            "
            v-if="movie.poster_path !== null"
            class="line_card"
          >
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
              <p>Жанр: {{ movie.genre_ids.join(" ") }} | {{ movieIndex }}</p>
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
          <vs-dialog
            scroll
            overflow-hidden
            blur
            not-close
            auto-width
            v-model="dialogs.data[genreIndex][movieIndex][movie.id]"
          >
            <template #header>
              <h3>{{ movie.name }}</h3>
            </template>
            <div class="con-content">
              <h4>Whats is Vuesax?</h4>
              <p>
                Vuesax (pronounced / vjusacksː /, as view sacks) is a framework
                of UI components created with Vuejs to make projects easily and
                with a unique and pleasant style, vuesax is created from scratch
                and designed for all types of developers from the frontend lover
                to the backend who wants to easily create their visual approach
                to the end-user We are focused on streamlining the work of the
                programmer by giving components created in their entirety and
                with independent customization and very easy to implement, so
                creativity is in our hands but we do not neglect that each
                project is different both visually and in its ecosystem Vuesax
                does not have a design line such as other component frameworks
                based on Material Design, we believe that there are already
                emaciated frameworks that look visually and in UI / UX and we
                don't want to be one more of the bunch, apart from that we love
                to create and design new experiences and surprise you with new
                elements or details that we can only do by being visually free.
              </p>

              <h4>Why Vuesax?</h4>

              <p>
                Vuesax is a relatively new framework with a refreshing design
                and in the latest trends, vuesax based on vuejs which means that
                we go hand in hand with one of the most popular javascript
                frameworks in the world and with a huge community with which you
                will have all the help and documentation to create and make your
                project
                <br />
                <br />
                - Vuesax, unlike many frameworks, is designed from scratch and
                we are not anchored to any design line, this is something great
                since your project is going to be unique and very different from
                the others

                <br />
                <br />
                - We are focused on the quick and easy creation of projects
                giving a beautiful visual line but without forgetting the
                personalization and independence of the developer

                <br />
                <br />
                - Vuesax uses native css variables for better customization and
                production changes such as changing to dark theme or changing
                the main color of the entire application with few javascript
                lines
                <br />
                <br />

                - Vuesax is a frame designed to have a great visual impact and
                that is always in trend with respect to design.
                <br />
                <br />

                - An open-source community to create, improve and correct any
                component or function.
                <br />
                <br />

                - Independent components to avoid importing unnecessary code.
                <br />
                <br />

                - Markdown documents for better sustainability.
                <br />
                <br />

                - and much more.
              </p>
            </div>
          </vs-dialog>
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
      dialogs: {
        data: [],
      },
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
    test(x) {
      console.log(x);
    },
  },
  created() {
    let genreData = [];
    axios
      .get(
        `https://api.themoviedb.org/3/tv/popular?api_key=52217232f795bbefbb1b7c951aae98ad&language=en-US`
      )
      .then((r) => {
        this.genres[0].series = r.data.results;
        let z = [];
        r.data.results.forEach((p) => {
          try {
            let obj = new Object();
            obj[`${p.id}`] = false;
            z.push(obj);
          } catch (error) {
            console.log(`ERR: `, error);
          }
        });
        genreData.push(z);
      });
    axios
      .get(
        `https://api.themoviedb.org/3/tv/top_rated?api_key=52217232f795bbefbb1b7c951aae98ad&language=en-US`
      )
      .then((x) => {
        this.genres[1].series = x.data.results;
        let y = [];
        x.data.results.forEach((p) => {
          try {
            let obj = new Object();
            obj[`${p.id}`] = false;
            y.push(obj);
          } catch (error) {
            console.log(`ERR: `, error);
          }
        });
        genreData.push(y);
      });
    this.dialogs.data = genreData;
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
