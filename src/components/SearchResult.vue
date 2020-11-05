<template>
  <div>
    <b-container fluid class="result" style=" background : #01011d">
      <div>
        <h2 style="color:white">
          Search results for <span style="color:#0000cd"> "{{ query }}"</span>
        </h2>
      </div>
      <b-row>
        <b-button
          pill
          variant="primary"
          class="btn-circle mt-4"
          @click="$router.go(-1)"
        >
          <b-icon icon="arrow-left"></b-icon>
        </b-button>
      </b-row>
      <div class="mt-4">
        <template v-if="shows.length > 0">
          <b-row>
            <b-col
              lg="3"
              md="4"
              sm="6"
              v-for="(show, index) in shows"
              :key="index"
            >
              <card v-bind:shows="show"> </card>
              <br />
            </b-col>
          </b-row>
        </template>
        <template v-else>
          <b-row class="mt-4">
            <b-col lg="3" md="4" v-for="i in 8" :key="i">
              <content-placeholders :rounded="true">
                <content-placeholders-img
                  style="height:295px ;width:210px ; "
                />
                <content-placeholders-text :lines="2" />
              </content-placeholders>
              <br />
            </b-col>
          </b-row>
        </template>
      </div>
    </b-container>
  </div>
</template>

<script>
import { searchMovie } from "../service/api";
import Card from "../components/Card";
export default {
  name: "SearchShows",
  components: {
    Card
  },
  data() {
    return {
      shows: [],
      query: this.$route.params.query
    };
  },
  created() {
    this.getSearchedShows();
  },
  methods: {
    getSearchedShows() {
      searchMovie(this.$route.params.query)
        .then(response => {
          this.shows = response.data;
          this.shows = this.shows.map(show => show.show);
          if (this.shows.length == 0)
            this.$router.push({
              name: "PageNotFound"
            });
        })
        .catch(err => console.log(err));
     }
   },
  watch: {
    $route() {
      this.getSearchedShows();
    }
  }
};
</script>

<style scoped>
.result {
  padding-left: 70px;
}
</style>