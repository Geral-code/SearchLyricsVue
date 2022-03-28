<template>
  <div class="container">
    <div class="titulo text-center mb-3 mt-5">
        <h1 class= "font-effect-shadow-multiple">LYRICS NOW!</h1>
    </div>

  
    <div class="row mt-5">
      <div class="col-12 text-center d-flex justify-content-center">
        <form @submit.prevent="submit">
          <div class="mb-3">
            <input
              class="form-control mb-3"
              type="text"
              v-model="artista"
              placeholder="Enter artist name"
            />
            <input
              class="form-control"
              type="text"
              v-model="cancion"
              placeholder="Enter song title"
               
            />
          </div>
          <button class="btn btn-danger mb-3 mt-3">Get the Lyrics</button>
        </form>
      </div>
    </div>
    <div class="container_cancion">
      <div class="row mt-5">
        <div class="col-12 text-center my-5">
         <p class="text-center mt-3 ">{{ lyrics }}</p>
        </div>
      </div>
    </div>
  </div>


</template>

<script>
import { consumirCanciones } from "./api";


export default {
  name: "App",
  components: {},
  data() {
    return {
      artista: "",
      cancion: "",
      lyrics: "",
    };
  },
  methods: {


    async submit() {
      try {
        if (this.artista != null && this.cancion != null) {
          let response = await consumirCanciones(this.artista, this.cancion);
          console.log(response.lyrics);

          if (this.lyrics == "") {
            let letra = await consumirCanciones(this.artista, this.cancion);
            this.lyrics = letra.lyrics;
          } else {
            this.lyrics = response.lyrics;
          }
        }
      } catch (error) {
        this.lyrics =
          "The song / artist does not exist or there is a typo somewhere ! Please check";
      }
    },
 
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Rubik+Mono+One&display=swap&effect=shadow-multiple');



#app {
  background:#522d5b;
}

html {
  font-family: 'Rubik Mono One', sans-serif;
  background: #522d5b;
  font-size: 1.200rem  !important;
}
h1 {
  color:  #d7385e;
  font-family: 'Rubik Mono One', sans-serif;
  font-size: 3.200rem !important;
   
}
p {
 color: white;
  white-space: pre-wrap;
  font-family: 'Rubik Mono One', sans-serif;
  font-size: 20px;


}
button {
  background: #d7385e !important;
}



</style>

