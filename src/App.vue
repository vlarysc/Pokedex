<template>
  <div id="app">
    <div class="search" :elevation="20">
      <form class="pokedex-control">
        <div class="form-control">
          <label for="filter-name"></label>
          <span>
            <input class="swing" id="song" type="text" v-model="busca" placeholder="Buscar Pokemon Pelo Nome" /><label
              for="song"
              >Pokemon</label
            >
          </span>
        </div>
        <div class="form-control2">
          <label for="filter-type">Tipo:</label>
          <select id="filter-type">
            <option value="">Todos</option>
          </select>
        </div>
      </form>
    </div>

    <img src="./assets/poke.png" width="450px" style="display:block; margin-left: auto; margin-right: auto;" />
    <h2 class="text">Pokedex</h2>
    <div class="column is-half">
      <div v-for="(pokemon, index) in resultSearch" :key="index">
        <Pokemon :name="pokemon.name" :url="pokemon.url" :id="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  name: "App",
  components: { Pokemon },
  data() {
    return {
      pokemons: [],
      busca: ""
    };
  },
  async created() {
    await axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then((res) => {
      // eslint-disable-next-line no-console
      console.log("pegou a lista pokemons");
      this.pokemons = res.data.results;
    });
    // eslint-disable-next-line no-console
    console.log(this.pokemons);
  },
  computed: {
    resultSearch() {
      if (this.busca == "" || this.busca == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter((pokemon) => pokemon.name == this.busca);
      }
    }
  }
};
</script>

<style>
.text {
  text-align: center;
  color: black;
}
body {
  font-family: arial, sans-serif;
  background: #2bc0e4; /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #eaecc6, #2bc0e4); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #eaecc6,
    #2bc0e4
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
.search {
  background: #fffc00; /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #fff783, #fffc00); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #fff783,
    #fffc00
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */

  border: 5px solid #53a4cf;
  margin-bottom: 30px;
  -webkit-box-shadow: 9px 7px 5px rgba(50, 50, 50, 0.77);
  -moz-box-shadow: 9px 7px 5px rgba(50, 50, 50, 0.77);
  box-shadow: 9px 7px 5px rgba(50, 50, 50, 0.77);
}

@import url(https://fonts.googleapis.com/css?family=Open+Sans:400, 700, 600, 300, 800);
* {
  box-sizing: border-box;
  margin: 0;
}

html,
body {
  overflow-x: hidden;
  font-family: "Open Sans", sans-serif;
  font-weight: 300;
  background: #2bc0e4; /* fallback for old browsers */
  background: -webkit-linear-gradient(to right, #eaecc6, #2bc0e4); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #eaecc6,
    #2bc0e4
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
.form-control2 {
  display: inline-block;
  margin-left: 600px;
  font-weight: 600;
  color: #364bc2;
  margin-bottom: 10px;
}
.form-control {
  padding: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.row {
  max-width: 800px;
  margin: 0 auto;
  padding: 60px 30px;
  background: #032429;
  position: relative;
  z-index: 1;
  text-align: center;
}
.row:before {
  position: absolute;
  content: "";
  display: block;
  top: 0;
  left: -5000px;
  height: 100%;
  width: 15000px;
  z-index: -1;
  background: inherit;
}
.row:first-child {
  padding: 40px 30px;
}
.row:nth-child(2),
.row:nth-child(8),
.row:nth-child(10) {
  background: #134a46;
}
.row:nth-child(3),
.row:nth-child(7) {
  background: #377d6a;
}
.row:nth-child(4),
.row:nth-child(6) {
  background: #7ab893;
}
.row:nth-child(5) {
  background: #b2e3af;
}
.row span {
  position: relative;
  display: inline-block;
  margin: 30px 10px;
}

.basic-slide {
  display: inline-block;
  width: 215px;
  padding: 10px 0 10px 15px;
  font-family: "Open Sans", sans;
  font-weight: 400;
  color: #377d6a;
  background: #efefef;
  border: 0;
  border-radius: 3px;
  outline: 0;
  text-indent: 70px;
  transition: all 0.3s ease-in-out;
}
.basic-slide::-webkit-input-placeholder {
  color: #efefef;
  text-indent: 0;
  font-weight: 300;
}
.basic-slide + label {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  top: 0;
  left: 0;
  padding: 10px 15px;
  text-shadow: 0 1px 0 rgba(19, 74, 70, 0.4);
  background: #7ab893;
  transition: all 0.3s ease-in-out;
  border-top-left-radius: 3px;
  border-bottom-left-radius: 3px;
}

.basic-slide:focus,
.basic-slide:active {
  color: #377d6a;
  text-indent: 0;
  background: #fff;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
.basic-slide:focus::-webkit-input-placeholder,
.basic-slide:active::-webkit-input-placeholder {
  color: #aaa;
}
.basic-slide:focus + label,
.basic-slide:active + label {
  transform: translateX(-100%);
}

.clean-slide {
  position: relative;
  display: inline-block;
  width: 215px;
  padding: 10px 0 10px 15px;
  font-family: "Open Sans", sans;
  font-weight: 400;
  color: #377d6a;
  background: #efefef;
  border: 0;
  border-radius: 3px;
  outline: 0;
  text-indent: 60px;
  transition: all 0.3s ease-in-out;
}
.clean-slide::-webkit-input-placeholder {
  color: #efefef;
  text-indent: 0;
  font-weight: 300;
}
.clean-slide + label {
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  transform: translateX(0);
  top: 0;
  left: 0;
  bottom: 0;
  padding: 13px 15px;
  font-size: 11px;
  font-weight: 700;
  text-transform: uppercase;
  color: #032429;
  text-align: left;
  text-shadow: 0 1px 0 rgba(255, 255, 255, 0.4);
  transition: all 0.3s ease-in-out, color 0.3s ease-out;
  border-top-left-radius: 3px;
  border-bottom-left-radius: 3px;
  overflow: hidden;
}
.clean-slide + label:after {
  display: flex;
  align-items: center;
  justify-content: center;
  content: "";
  position: absolute;
  top: 0;
  right: 100%;
  bottom: 0;
  width: 100%;
  background: #7ab893;
  z-index: -1;
  transform: translate(0);
  transition: all 0.3s ease-in-out;
  border-top-left-radius: 3px;
  border-bottom-left-radius: 3px;
}

.clean-slide:focus,
.clean-slide:active {
  color: #377d6a;
  text-indent: 0;
  background: #fff;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
.clean-slide:focus::-webkit-input-placeholder,
.clean-slide:active::-webkit-input-placeholder {
  color: #aaa;
}
.clean-slide:focus + label,
.clean-slide:active + label {
  color: #fff;
  text-shadow: 0 1px 0 rgba(19, 74, 70, 0.4);
  transform: translateX(-100%);
}
.clean-slide:focus + label:after,
.clean-slide:active + label:after {
  transform: translate(100%);
}

.gate {
  display: inline-block;
  width: 215px;
  padding: 10px 0 10px 15px;
  font-family: "Open Sans", sans;
  font-weight: 400;
  color: #377d6a;
  background: #efefef;
  border: 0;
  border-radius: 3px;
  outline: 0;
  text-indent: 65px;
  transition: all 0.3s ease-in-out;
}
.gate::-webkit-input-placeholder {
  color: #efefef;
  text-indent: 0;
  font-weight: 300;
}
.gate + label {
  display: inline-block;
  position: absolute;
  top: 0;
  left: 0;
  padding: 10px 15px;
  text-shadow: 0 1px 0 rgba(19, 74, 70, 0.4);
  background: #7ab893;
  transition: all 0.4s ease-in-out;
  border-top-left-radius: 3px;
  border-bottom-left-radius: 3px;
  transform-origin: left bottom;
  z-index: 99;
}
.gate + label:before,
.gate + label:after {
  content: "";
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  border-radius: 3px;
  background: #377d6a;
  transform-origin: left bottom;
  transition: all 0.4s ease-in-out;
  pointer-events: none;
  z-index: -1;
}
.gate + label:before {
  background: rgba(3, 36, 41, 0.2);
  z-index: -2;
  right: 20%;
}

span:nth-child(2) .gate {
  text-indent: 85px;
}

span:nth-child(2) .gate:focus,
span:nth-child(2) .gate:active {
  text-indent: 0;
}

.gate:focus,
.gate:active {
  color: #377d6a;
  text-indent: 0;
  background: #fff;
  border-top-right-radius: 3px;
  border-bottom-right-radius: 3px;
}
.gate:focus::-webkit-input-placeholder,
.gate:active::-webkit-input-placeholder {
  color: #aaa;
}
.gate:focus + label,
.gate:active + label {
  transform: rotate(-66deg);
  border-radius: 3px;
}
.gate:focus + label:before,
.gate:active + label:before {
  transform: rotate(10deg);
}

.skinny {
  display: inline-block;
  width: 215px;
  padding: 10px 0 10px 15px;
  font-family: "Open Sans", sans;
  font-weight: 400;
  color: #377d6a;
  background: #efefef;
  border: 0;
  border-radius: 3px;
  outline: 0;
  text-indent: 75px;
  transition: all 0.3s ease-in-out;
}
.skinny::-webkit-input-placeholder {
  color: #efefef;
  text-indent: 0;
  font-weight: 300;
}
.skinny + label {
  display: inline-block;
  position: absolute;
  transform: translateX(0);
  top: 0;
  left: 0;
  padding: 10px 15px;
  text-shadow: 0 1px 0 rgba(19, 74, 70, 0.4);
  transition: all 0.3s ease-in-out;
  border-top-left-radius: 3px;
  border-bottom-left-radius: 3px;
  overflow: hidden;
}
.skinny + label:before,
.skinny + label:after {
  content: "";
  position: absolute;
  right: 0;
  left: 0;
  z-index: -1;
  transition: all 0.3s ease-in-out;
}
.skinny + label:before {
  top: 5px;
  bottom: 5px;
  background: #377d6a;
  border-top-left-radius: 3px;
  border-bottom-left-radius: 3px;
}
.skinny + label:after {
  top: 0;
  bottom: 0;
  background: #377d6a;
}

.skinny:focus,
.skinny:active {
  color: #377d6a;
  text-indent: 0;
  background: #fff;
}
.skinny:focus::-webkit-input-placeholder,
.skinny:active::-webkit-input-placeholder {
  color: #aaa;
}
.skinny:focus + label,
.skinny:active + label {
  transform: translateX(-100%);
}
.skinny:focus + label:after,
.skinny:active + label:after {
  transform: translateX(100%);
}

.slide-up {
  display: inline-block;
  width: 215px;
  padding: 10px 0 10px 15px;
  font-family: "Open Sans", sans;
  font-weight: 400;
  color: #377d6a;
  background: #efefef;
  border: 0;
  border-radius: 3px;
  outline: 0;
  text-indent: 80px;
  transition: all 0.3s ease-in-out;
}
.slide-up::-webkit-input-placeholder {
  color: #efefef;
  text-indent: 0;
  font-weight: 300;
}
.slide-up + label {
  display: inline-block;
  position: absolute;
  transform: translateX(0);
  top: 0;
  left: 0;
  padding: 10px 15px;
  text-shadow: 0 1px 0 rgba(19, 74, 70, 0.4);
  transition: all 0.3s ease-in-out;
  border-top-left-radius: 3px;
  border-bottom-left-radius: 3px;
  overflow: hidden;
}
.slide-up + label:before,
.slide-up + label:after {
  content: "";
  position: absolute;
  right: 0;
  left: 0;
  z-index: -1;
  transition: all 0.3s ease-in-out;
}
.slide-up + label:before {
  top: 6px;
  left: 5px;
  right: 5px;
  bottom: 6px;
  background: #377d6a;
}
.slide-up + label:after {
  top: 0;
  bottom: 0;
  background: #377d6a;
}

span:nth-child(1) .slide-up {
  text-indent: 105px;
}

span:nth-child(3) .slide-up {
  text-indent: 125px;
}

span:nth-child(1) .slide-up:focus,
span:nth-child(1) .slide-up:active,
span:nth-child(3) .slide-up:focus,
span:nth-child(3) .slide-up:active {
  text-indent: 0;
}

.slide-up:focus,
.slide-up:active {
  color: #377d6a;
  text-indent: 0;
  background: #fff;
}
.slide-up:focus::-webkit-input-placeholder,
.slide-up:active::-webkit-input-placeholder {
  color: #aaa;
}
.slide-up:focus + label,
.slide-up:active + label {
  transform: translateY(-100%);
}
.slide-up:focus + label:before,
.slide-up:active + label:before {
  border-radius: 5px;
}
.slide-up:focus + label:after,
.slide-up:active + label:after {
  transform: translateY(100%);
}

.card-slide {
  display: inline-block;
  width: 215px;
  padding: 10px 0 10px 15px;
  font-family: "Open Sans", sans;
  font-weight: 400;
  color: #377d6a;
  background: #efefef;
  border: 0;
  border-radius: 3px;
  outline: 0;
  text-indent: 115px;
  transition: all 0.3s ease-in-out;
}
.card-slide::-webkit-input-placeholder {
  color: #efefef;
  text-indent: 0;
  font-weight: 300;
}
.card-slide + label {
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  padding: 10px 15px;
  text-shadow: 0 1px 0 rgba(19, 74, 70, 0.4);
  background: #7ab893;
  transition: all 0.3s ease-in-out;
  border-top-left-radius: 3px;
  border-bottom-left-radius: 3px;
  transform-origin: right center;
  transform: perspective(300px) scaleX(1) rotateY(0deg);
}

span:nth-child(2) .card-slide {
  text-indent: 55px;
}

span:nth-child(3) .card-slide {
  text-indent: 150px;
}

span:nth-child(2) .card-slide:focus,
span:nth-child(2) .card-slide:active,
span:nth-child(3) .card-slide:focus,
span:nth-child(3) .card-slide:active {
  text-indent: 0;
}

.card-slide:focus,
.card-slide:active {
  color: #377d6a;
  text-indent: 0;
  background: #fff;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
.card-slide:focus::-webkit-input-placeholder,
.card-slide:active::-webkit-input-placeholder {
  color: #aaa;
}
.card-slide:focus + label,
.card-slide:active + label {
  transform: perspective(600px) translateX(-100%) rotateY(80deg);
}

.swing {
  -webkit-box-shadow: 9px 7px 5px rgba(50, 50, 50, 0.77);
  -moz-box-shadow: 9px 7px 5px rgba(50, 50, 50, 0.77);
  box-shadow: 9px 7px 5px rgba(50, 50, 50, 0.77);
  width: 415px;
  margin-right: 0 100px;
  padding: 10px 0 10px 15px;
  font-family: "Open Sans", sans;
  font-weight: 400;
  color: #377d6a;
  background: #efefef;
  border: 0;
  border-radius: 8px;
  outline: 0;
  text-indent: 60px;
  transition: all 0.3s ease-in-out;
  display: flex;
  align-items: center;
  justify-content: center;
}
.swing::-webkit-input-placeholder {
  color: #efefef;
  text-indent: 0;
  font-weight: 300;
}
.swing + label {
  margin-left: 465px;
  margin-top: 25px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  top: 0;
  left: 0;
  padding: 10px 15px;
  text-shadow: 0 1px 0 rgba(19, 74, 70, 0.4);
  background: #1267b8;
  color: white;
  border-top-left-radius: 3px;
  border-bottom-left-radius: 3px;
  border-radius: 8px;
  transform-origin: 2px 2px;
  transform: rotate(0);
  animation: swing-back 0.4s 1 ease-in-out;
}

@keyframes swing {
  0% {
    transform: rotate(0);
  }
  20% {
    transform: rotate(116deg);
  }
  40% {
    transform: rotate(60deg);
  }
  60% {
    transform: rotate(98deg);
  }
  80% {
    transform: rotate(76deg);
  }
  100% {
    transform: rotate(82deg);
  }
}
@keyframes swing-back {
  0% {
    transform: rotate(82deg);
  }
  100% {
    transform: rotate(0);
  }
}
.swing:focus,
.swing:active {
  color: #377d6a;
  text-indent: 0;
  background: #fff;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
.swing:focus::-webkit-input-placeholder,
.swing:active::-webkit-input-placeholder {
  color: #aaa;
}
.swing:focus + label,
.swing:active + label {
  animation: swing 1.4s 1 ease-in-out;
  transform: rotate(82deg);
}

.balloon {
  display: inline-block;
  width: 215px;
  padding: 10px 0 10px 15px;
  font-family: "Open Sans", sans;
  font-weight: 400;
  color: #377d6a;
  background: #efefef;
  border: 0;
  border-radius: 3px;
  outline: 0;
  text-indent: 60px;
  transition: all 0.3s ease-in-out;
}
.balloon::-webkit-input-placeholder {
  color: #efefef;
  text-indent: 0;
  font-weight: 300;
}
.balloon + label {
  display: inline-block;
  position: absolute;
  top: 8px;
  left: 0;
  bottom: 8px;
  padding: 5px 15px;
  color: #032429;
  font-size: 11px;
  font-weight: 700;
  text-transform: uppercase;
  text-shadow: 0 1px 0 rgba(19, 74, 70, 0);
  transition: all 0.3s ease-in-out;
  border-radius: 3px;
  background: rgba(122, 184, 147, 0);
}
.balloon + label:after {
  position: absolute;
  content: "";
  width: 0;
  height: 0;
  top: 100%;
  left: 50%;
  margin-left: -3px;
  border-left: 3px solid transparent;
  border-right: 3px solid transparent;
  border-top: 3px solid rgba(122, 184, 147, 0);
  transition: all 0.3s ease-in-out;
}

.balloon:focus,
.balloon:active {
  color: #377d6a;
  text-indent: 0;
  background: #fff;
}
.balloon:focus::-webkit-input-placeholder,
.balloon:active::-webkit-input-placeholder {
  color: #aaa;
}
.balloon:focus + label,
.balloon:active + label {
  color: #fff;
  text-shadow: 0 1px 0 rgba(19, 74, 70, 0.4);
  background: #7ab893;
  transform: translateY(-40px);
}
.balloon:focus + label:after,
.balloon:active + label:after {
  border-top: 4px solid #7ab893;
}
</style>
