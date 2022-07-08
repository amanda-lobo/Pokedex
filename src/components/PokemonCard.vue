<template>
  <div class="card">
    <div class="img">
      <img :src="currentImg" :alt="name" >
    </div>
    <div class="rodape">
      <div class="name">
        <p>{{name}}</p>
      </div>
      <div class="number">
        <p>#{{index}}</p>
      </div>
    </div>
  </div>
</template>

<script>
  import api from '../services/api';
export default {
  name: 'Pokemon',
  props: {
    name: String,
    index: Number,
    url: String
  },
  created: function() {
    api.get(this.url).then((response) => {
      this.pokemon.type = response.data.types[0].type.name;
      this.pokemon.front = response.data.sprites.front_default;
      this.pokemon.back = response.data.sprites.back_default;
      this.currentImg = response.data.sprites.front_default;
    });
  },
  data() {
    return {
      isFront: true,
      currentImg: '',
      pokemon: {
        type: '',
        front: '',
        back: '',
      }
    }
  },
  methods: {
    changeSprite: function() {
      if(this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    }
  },
  filters: {
    upperCase: function(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  }
}
</script>

<style>
* {
  border: 0;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.card {
  width: 210px;
  height: 150px;
  background-color: white;
  margin: 7px;
  display: flex;
  justify-content: center;
  flex-direction: column;
  border-radius: 5px;
  -webkit-box-shadow: 0px 1px 2px 1px rgba(199, 199, 199, 0.78);
  box-shadow: 0px 1px 2px 1px rgba(199, 199, 199, 0.78);
}

.img {
  width: 100%;
  height: 80%;
  display: flex;
  justify-content: center;
}

.rodape {
  width: 100%;
  height: 20%;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}

.name {
  width: 80%;
  height: 100%;
  display: flex;
  align-items: center;
  margin: 5px;
}

.number {
  width: 20%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: end;
  margin: 5px;
}

.name p {
  margin: 5px;
  color: #81807a;
}

.number p {
  margin: 5px;
  color: #81807a;
}
</style>