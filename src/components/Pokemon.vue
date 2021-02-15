<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img :src="currentImg" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} - {{ name }}</p>
            <p class="subtitle is-6">
              {{ pokemon.type[0] }} {{ pokemon.type[1] }}
            </p>
          </div>
        </div>
        <div class="content">
             <button class="button is-link is-light" @click="mudarSprite">Mudar Sprite</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemon.type[0] = res.data.types[0].type.name;
      if (res.data.types.length > 1) {
        this.pokemon.type[1] = res.data.types[1].type.name;
      }
      this.pokemon.back = res.data.sprites.back_default;
      this.pokemon.front = res.data.sprites.front_default;
      this.currentImg = this.pokemon.front

      console.log(this.pokemon);
    });
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        type: ["", ""],
        front: "",
        back: "",
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  methods: {
      mudarSprite: function () {
          if (this.isFront) {
              this.isFront = false;
              this.currentImg = this.pokemon.back
          }else{
              this.isFront = true
              this.currentImg = this.pokemon.front
          }
      }
  }
  };
</script>

<style>
#pokemon {
  margin-top: 6%;
}
</style>