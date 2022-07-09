<template>
  <div class="card">
    <div class="img">
      <img :src="currentImg" :alt="name" />
    </div>
    <div class="rodape">
      <div class="name">
        <p>{{ name }}</p>
      </div>
      <div class="number">
        <p>#{{ index }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import "../PokemonCard/PokemonCard.scss";
export default {
  name: "Pokemon",
  props: {
    name: String,
    index: Number,
    url: String,
  },
  created: function () {
    this.apiCall();
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        type: "",
        front: "",
        back: "",
      },
    };
  },
  watch: {
    url(newUrl, oldUrl) {
      this.apiCall();
    },
  },
  methods: {
    changeSprite: function () {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    },
    apiCall: function () {
      fetch(this.url)
        .then((response) => response.json())
        .then((data) => {
          this.pokemon.type = data.types.map((e) => e.type.name).join(", ");
          this.pokemon.front = data.sprites.front_default;
          this.pokemon.back = data.sprites.back_dafult;
          this.currentImg = data.sprites.front_default;
        });
    },
  },
  filters: {
    upperCase: function (value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
};
</script>
