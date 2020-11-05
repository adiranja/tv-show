<template>
  <div class="mt-8">
    <router-link
      :to="{
        name: 'ShowDetail',
        params: { id: shows.id }
      }"
    >
      <img
        v-bind:src="shows.image.medium || shows.image.original"
        v-if="shows.image"
      />
      <div v-else>
        <content-placeholders :rounded="true">
          <content-placeholders-img style="height:295px ;width:210px ; " />
        </content-placeholders>
      </div>
    </router-link>
    <div class="mt-1" v-if="shows.name">
      <router-link
        :to="{
          name: 'ShowDetail',
          params: { id: shows.id }
        }"
        >{{ shows.name }}
      </router-link>
      <div class="mt-1">
        <span>
          <b-icon style="color:yellow" icon="star-fill " class="mx-1"></b-icon>
        </span>
        <span class=" show-average" style="color:white">
          {{ shows.rating.average }}
        </span>
        <span class="mx-2" style="color:white">|</span>
        <span class="show-premiered" style="color:white">
          {{ shows.premiered }}
        </span>
      </div>
      <div class="show-genres" style="color:white">
        {{ shows.genres.join(", ") }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["shows"]
};
</script> 

<style scoped>
.spinner {
  width: 3rem;
  height: 3rem;
  margin-top: 40%;
  margin-left: 10%;
}
</style>
