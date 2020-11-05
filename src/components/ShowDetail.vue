<template>
  <div style=" background : #01011d">
    <b-container fluid style="min-height:100vh">
      <div>
        <b-button pill variant="primary" class="mt-4" @click="$router.go(-1)">
          <b-icon icon="arrow-left"></b-icon>
        </b-button>
      </div>
      <b-row class=" mt-4" align-h="center">
        <b-col lg="4" md="6" sm="6">
          <b-img
            v-if="show.image"
            left
            fluid
            width="300%"
            v-bind:src="show.image.medium || show.image.original"
            rounded
          ></b-img>
          <div v-else>
            <content-placeholders :rounded="true">
              <content-placeholders-img
                style="height:295px ;width:210px ;   "
              />
            </content-placeholders>
          </div>
        </b-col>
        <b-col lg="8" md="6" sm="6">
          <h2 class="show-name mt-4" style="color:#007bff">{{ show.name }}</h2>
          <div>
            <div v-if="this.rating">
              <span>
                <b-icon icon="star-fill" style="color:yellow"></b-icon>
              </span>
              <span class="show-detail ml-2">
                {{ show.rating.average }}
              </span>
            </div>
            <div v-else>
              <span>
                <b-icon icon="star-fill" style="color:yellow"></b-icon>
              </span>
              <span class="show-detail ml-2">
                NA
              </span>
            </div>
            <div v-if="this.premiered">
              <span><b-icon icon="calendar3" class="icon"></b-icon> </span>
              <span class="show-detail ml-2"> {{ show.premiered }}</span>
            </div>
            <div v-else>
              <span><b-icon icon="calendar3" class="icon"></b-icon> </span>
              <span class="show-detail ml-2"> NA</span>
            </div>
            <div v-if="this.genre.length>0">
              <span><b-icon icon="film" class="icon"></b-icon></span>
              <span class="show-detail ml-2"> {{ show.genres.join() }}</span>
            </div>
             <div v-else>
             <span><b-icon icon="film" class="icon"></b-icon></span>
              <span class="show-detail ml-2"> NA</span>
            </div>
          </div>
          <div class="mt-3  show-detail ">
            <p v-html="show.summary"></p>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import { getMovieDetails } from "../service/api";
export default {
  name: "ShowDetails",
  data() {
    return {
      show: {},
      rating:"",
      premiered:"",
      genre:""
    };
  },
  created() {
    getMovieDetails(this.$route.params.id)
      .then(response => {
        this.show = response.data;
        this.rating=this.show.rating.average;
        this.premiered=this.show.premiered;
        this.genre=this.show.genres 
      })
      .catch(() => {
        this.$router.push({
          name: "PageNotFound"
        });
      });
    }
} ;
</script>

<style scoped>
.spin {
  width: 6rem;
  height: 6rem;
  margin-top: 10%;
  margin-left: 10%;
  color: white;
}
.show-detail {
  color: white;
}
.icon {
  color: #0000cd;
}
</style>