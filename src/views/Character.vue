<template>
  <div class="character_card_container">
    <div class="character_card_body" >
      <div class="character_card_img" v-if="character">
        <img :src='character.image' alt="" />
      </div>
      <v-sheet
        class="character_card_img"
        :color="`grey lighten-4`"
        v-else
      >
        <v-skeleton-loader
          type="image"
        ></v-skeleton-loader>
      </v-sheet>

        <v-list class="character_card_info" v-if="character">
          <v-list-item>
            <span class="name" v-text="character.name"></span>
          </v-list-item>
          <v-list-item>
            Gender: <span v-text="character.gender"></span>
          </v-list-item>
          <v-list-item>
            Species: <span v-text="character.species"></span>
          </v-list-item>
          <v-list-item>
            Status: <span v-text="character.status"></span>
          </v-list-item>
          <v-list-item>
            Location: <span v-text="character.location.name"></span>
          </v-list-item>
          <v-list-item>
            Origin: <span v-text="character.origin.name"></span>
          </v-list-item>
        </v-list>
      <v-sheet
        class="character_card_info"
        :color="`grey lighten-4`"
        v-else
      >
        <v-skeleton-loader
          max-width="200"
          type="list-item,list-item,list-item,list-item,list-item,list-item"
        ></v-skeleton-loader>
      </v-sheet>
    </div>
    <router-link to='/' class="back_to_list_btn" >
        Back to List of characters
    </router-link>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Character',
  data() {
    return {
      character: null,
    };
  },
  mounted() {
    axios
      .get(`https://rickandmortyapi.com/api/character/${this.$route.params.id}`)
      .then((response) => {
        this.character = response.data;
      });
  },
};
</script>

<style lang="scss">
.character_card_container {
  margin-top: 20px;
  color: #0f0302;
  font-family: "Ranchers", cursive;
}
.character_card_body {
  height: 500px;
  width: 60%;
  border-radius: 10px;
  margin: auto;
  background-color: rgb(255, 245, 245);
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr;
  gap: 1px 1px;
  grid-template-areas: ". .";
  justify-items: normal;
  align-items: center;
  .character_card_info {
    justify-self: end;
    background: none;
    padding: 2rem;
    width: 100%;
    margin: 2rem;
    float: right;
    font-size: 1.2rem;
    h1 {
      font-size: 3rem;
      text-transform: uppercase;
      margin-top: 0;
      letter-spacing: 0.3rem;
    }
  }
  .character_card_img {
    width: 300px;
    height: 300px;
    justify-self: center;
    img {

      border-radius: 10px;
    }
  }
}
.v-skeleton-loader__image {
  height: 300px;
}
.back_to_list_btn {
  background-color: brown;
  color: black !important;
  position: relative;
  margin: 50px auto;
  height: 100px;
  width: 60%;
  border: 0 solid #e5e5e5;
  overflow: hidden;
  display: block;
  cursor: pointer;
  box-shadow: 0 2px 2px 0 rgba(252, 252, 252, 0.5),
  0 0 0 3px rgba(255, 255, 255, 0.5);
  border-radius: 8px;
  text-align: center;
  text-indent: 20px;
  text-decoration: none;
  font-size: 3.5rem;
  font-family: "Ranchers", cursive;
}
.v-skeleton-loader__list-item {
  background: none !important;
}

.name{
  font-size: 40px;
  font-weight: bold;
}
</style>
