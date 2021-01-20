<template>
  <div id="pokemon" :class="pokemon.type">
    <v-card class="mx-auto" max-width="344">
      <v-card-text class="vip" :class="pokemon.type">
        <div class="card-image">
          <figure class="image">
            <img
              class="photo"
              :src="currentImg"
              alt="Frente do pokemon"
              style="display:block; margin-left: auto; margin-right: auto;"
            />
          </figure>
        </div>

        <div class="text--primary">
          <div>
            <h1 style="display:block; margin-left: auto; margin-right: auto;">{{ id }} - {{ name | upper }}</h1>
            <h3>{{ pokemon.type }}</h3>
          </div>
        </div>
        <v-card-actions>
          <v-btn
            text
            color="blue accent-4 white--text"
            @click="changeSprite"
            style="display:block; margin-left: auto; margin-right: auto; padding: 5px; margin-top: 3px;"
          >
            Inverter Imagem
          </v-btn>
        </v-card-actions>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  created: function() {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
    });
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        type: "",
        front: "",
        back: ""
      }
    };
  },
  methods: {
    changeSprite() {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    }
  },
  props: {
    id: Number,
    name: String,
    url: String
  },
  filters: {
    upper: function(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  }
};
</script>

<style>
#pokemon {
  display: inline-block;
  width: 20%;
  min-width: 150px;
  margin-top: 100px;
  float: left;
  margin-top: 3%;
  margin-left: 4%;
  padding: 5px;
  border: 5px solid #ffffff;
  -webkit-box-shadow: 9px 7px 5px rgba(50, 50, 50, 0.77);
  -moz-box-shadow: 9px 7px 5px rgba(50, 50, 50, 0.77);
  box-shadow: 9px 7px 5px rgba(50, 50, 50, 0.77);
}
.photo {
  width: 200px;
  height: 200px;
}

.ground {
  background-color: #a4acaf;
  color: #212121 !important;
}

.normal {
  background-color: #f6ffa4;
  color: #554d33 !important;
}

.dragon {
  background: linear-gradient(180deg, #53a4cf 50%, #f16e57 50%);
  background-color: #53a4cf;
  color: #fff !important;
}

.grass {
  background-color: #9bcc50;
  color: #212121 !important;
}

.poison {
  background-color: #b97fc9;
  color: #fff !important;
}

.fire {
  background-color: #fd7d24;
  color: #fff !important;
}

.water {
  background-color: #4592c4;
  color: #fff !important;
}

.electric {
  background-color: #eed535;
  color: #212121 !important;
}

.bug {
  background-color: #729f3f;
  color: #fff !important;
}

.flying {
  background: linear-gradient(180deg, #3dc7ef 50%, #bdb9b8 50%);
  background-color: #3dc7ef;
  color: #212121 !important;
}

.fairy {
  background-color: #fdb9e9;
  color: #212121 !important;
}

.psychic {
  background-color: #f366b9;
  color: #fff !important;
}

.rock {
  background-color: #a38c21;
  color: #fff !important;
}

.ice {
  background-color: #51c4e7;
  color: #212121 !important;
}

.ghost {
  background-color: #7b62a3;
  color: #fff !important;
}

.steel {
  background-color: #9eb7b8;
  color: #212121 !important;
}

.fighting {
  background-color: #d56723;
  color: #fff !important;
}
</style>
