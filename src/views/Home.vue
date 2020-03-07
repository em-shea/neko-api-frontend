<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <div class="container main-container">
      <div class="row pt-5 pb-1">
        <div class="col">
          <h3>Neko Atsume API</h3>
          <img class="header-img" alt="Pickles" title="Pickles" src="https://neko-atsume.s3.amazonaws.com/img/Pickles.jpg">
        </div>
      </div>
      <div class="row py-3">
        <div class="col">
          <p>Get data on cats and goodies from <a href="https://www.nekoatsume.com/en/">Neko Atsume: Kitty Collector</a>.</p>
          <!-- <p><a href="#docs">Docs</a></p> -->
        </div>
      </div>
      <!-- Need to add scroll spy? -->
      <!-- <div class="row py-3">
        <div class="col">
          <div v-for="cat in this.cats" :key="cat.CatId">
            {{ cat.CatName }}
            <div>
              <img class="cat-img" v-bind:src="cat.CatImage">
            </div>
          </div>
        </div>
      </div> -->
      <div class="row py-3">
        <div class="col-12">
          <p>Try it out:</p>
        </div>
        <div class="col-12">
          <div class="row">
            <div class="input-group mb-3">
              <div class="input-group-prepend">
                <span class="input-group-text" id="basic-addon3">https://api.neko-atsume.emshea.com/</span>
              </div>
              <input type="text" class="form-control" id="basic-url" aria-describedby="basic-addon3" v-model="testInput">
              <div class="input-group-append">
                <button class="btn btn-outline-secondary" type="button" id="button-addon2" v-on:click="getTestResponse()">Submit</button>
              </div>
            </div>
          </div>
          <div class="row">
            <p>Try <button class="btn btn-link test-options" v-on:click="testInput = 'cats/18', getTestResponse()">cats/18</button>, cats/pumpkin, goodies/10</p>
          </div>
        </div>
      </div>
      <div class="row json">
      <div class="col border">
        <tree-view :data="testResponse" :options="{maxDepth: 3}"></tree-view>
      </div>
    </div>
    <docs></docs>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import docs from '@/components/docs.vue'

export default {
  name: 'Home',
  components: {
    docs
  },
  data () {
    return {
      cats: null,
      testInput: 'cats/4',
      testUrl: null,
      testResponse: null
    }
  },
  mounted () {
    this.getTestResponse()
  },
  methods: {
    // getCats () {
    //   return axios
    //     .get('https://neko-atsume.emshea.com/api/cats', {}
    //     )
    //     .then((response) => {
    //       this.cats = response.data
    //       console.log(this.cats)
    //     })
    // },
    getTestResponse () {
      this.testUrl = 'https://api.neko-atsume.emshea.com/' + this.testInput
      return axios
        .get(this.testUrl, {}
        )
        .then((response) => {
          this.testResponse = response.data
        }).catch((error) => {
          this.testResponse = 'Request failed.'
          console.log(error)
        })
    }
  }
}

// axios.get('/user/1').then((response) => {
//     console.log('Everything is awesome.');
// }).catch((error) => {
//     console.warn('Not good man :(');
// })
</script>

<style scoped>
.header-img {
  width: 40px;
}
.cat-img {
  width: 40px;
}
.json {
  text-align: left;
}
.test-options {
  padding: 0;
}
.main-container {
  max-width: 65%;
}
@media(max-width:767px){
  .main-container {
    max-width: 80%;
  }
}
@media(min-width:768px){

}
@media(min-width:992px){

}
@media(min-width:1200px){

}

</style>
