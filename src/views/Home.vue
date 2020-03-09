<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <div class="container main-container px-0">
      <div class="row pt-5 pb-1">
        <div class="col">
          <h3>Neko Atsume API</h3>
          <img class="header-img" alt="Pickles" title="Pickles" src="https://neko-atsume.s3.amazonaws.com/img/Pickles.jpg">
        </div>
      </div>
      <div class="row py-3">
        <div class="col">
          <p>Get data on cats and goodies from <a href="https://www.nekoatsume.com/en/">Neko Atsume: Kitty Collector</a>.</p>
        </div>
      </div>

      <div class="row py-3">
        <div class="col">
          <h5>Try it out:</h5>
        </div>
      </div>

      <div class="row input-group-desktop">
        <div class="col">
          <div class="input-group mb-3">
            <div class="input-group-prepend">
              <span class="input-group-text" id="basic-addon3">https://api.neko-atsume.emshea.com/</span>
            </div>
            <input type="text" class="form-control" id="basic-url" aria-describedby="basic-addon3" v-model="testInput">
            <div class="input-group-append">
              <button class="btn btn-outline-secondary" type="button" id="button-addon2" v-on:click="getTestResponse()">Submit</button>
            </div>
          </div>

          <div class="row input-group-mobile">
            <div class="input-group mb-3">
              <div class="input-group-prepend px-0 col">
                <span class="input-group-text" id="basic-addon3">https://api.neko-atsume.emshea.com/</span>
              </div>
              <input type="text" class="form-control" id="basic-url" aria-describedby="basic-addon3" v-model="testInput">
              <div class="input-group-append">
                <button class="btn btn-outline-secondary" type="button" id="button-addon2" v-on:click="getTestResponse()">Submit</button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col test-options">
          <p>Try
            <button class="btn btn-link test-options-btn" v-on:click="testInput = 'cats/18', getTestResponse()"> cats/18</button>,
            <button class="btn btn-link test-options-btn" v-on:click="testInput = 'cats/pumpkin', getTestResponse()"> cats/pumpkin</button>,
            goodies/10.
          </p>
        </div>
      </div>

      <div class="row json">
        <div class="col scrollbar-y border mx-3">
          <tree-view :data="testResponse" :options="{maxDepth: 3}"></tree-view>
        </div>
      </div>
    <docs></docs>
    <hr>
    <div class="row">
      <div class="col footer">
        <p>Made with ❤️ by <a href="emshea.com">Emily</a>.</p>
      </div>
    </div>
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
      this.testResponse = 'loading...'
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
.scrollbar-y {
  height: 212px;
  overflow-y: auto;
}
.footer {
  text-align: left;
}
.test-options {
  text-align: left;
}
.test-options-btn {
  padding: 0;
}
.input-group-mobile .input-group-text {
  width: 100%
}
.input-group-mobile {
    visibility: hidden;
    display: none;
}
.main-container {
  max-width: 50%;
}
@media(max-width:767px){
  .main-container {
    max-width: 80%;
  }
}
@media(max-width:850px){
  .input-group-desktop {
    visibility: hidden;
    display: none;
  }
  .input-group-mobile {
    visibility: visible;
    display: flex;
  }
}
@media(min-width:992px){

}
@media(min-width:1200px){

}

</style>
