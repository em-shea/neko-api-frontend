<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <div class="container main-container px-0">

      <div class="row pt-5 pb-1">
        <div class="col">
          <h3>Neko Atsume API</h3>
          <!-- Add button to click to change header cat img -->
          <img class="header-img" v-bind:alt="catImgName" v-bind:title="catImgName" v-bind:src="catImg" v-on:click="switchCatImg()">
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
        </div>
      </div>

      <div class="row input-group-mobile">
        <div class="col">
          <div class="input-group mb-3">
            <div class="input-group-prepend px-0 col-12">
              <span class="input-group-text" id="basic-addon3">https://api.neko-atsume.emshea.com/</span>
            </div>
            <input type="text" class="form-control" id="basic-url" aria-describedby="basic-addon3" v-model="testInput">
            <div class="input-group-append">
              <button class="btn btn-outline-secondary" type="button" id="button-addon2" v-on:click="getTestResponse()">Submit</button>
            </div>
          </div>
        </div>
      </div>

      <div class="row">
        <div class="col test-options">
          <p>Try
            <button class="btn btn-link test-options-btn" v-on:click="testInput = 'cats/25', getTestResponse()"> cats/25 </button>,
            <button class="btn btn-link test-options-btn" v-on:click="testInput = 'cats/pumpkin', getTestResponse()"> cats/pumpkin</button>,
            <button class="btn btn-link test-options-btn" v-on:click="testInput = 'goodies/17', getTestResponse()"> goodies/17</button>, or
            <button class="btn btn-link test-options-btn" v-on:click="testInput = 'goodies/kotatsu', getTestResponse()"> goodies/kotatsu</button>.
          </p>
        </div>
      </div>

      <div class="row json">
        <div class="col scrollbar-y border mx-3">
          <tree-view :data="testResponse" :options="{maxDepth: 3, link: true}"></tree-view>
        </div>
      </div>
      <docs v-bind:cats="allCats" v-bind:goodies="allGoodies"></docs>
      <hr>
      <div class="row">
        <div class="col footer">
          <p>Made with &hearts; by <a href="https://emshea.com">Emily</a>.</p>
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
      allCats: null,
      allGoodies: null,
      catImg: 'https://neko-atsume.s3.amazonaws.com/img/Pickles.jpg',
      catImgName: 'Pickles',
      testInput: 'cats/9',
      testUrl: null,
      testResponse: null
    }
  },
  mounted () {
    this.getTestResponse()
    this.getCats()
    this.getGoodies()
  },
  methods: {
    getTestResponse () {
      this.testResponse = 'loading...'
      this.testUrl = 'https://api.neko-atsume.emshea.com/' + this.testInput
      return axios
        .get(this.testUrl, {}
        )
        .then((response) => {
          this.testResponse = response.data
        }).catch((error) => {
          this.testResponse = error.response.data
          console.log(error)
        })
    },
    getCats () {
      this.allCats = 'loading...'
      return axios
        .get('https://api.neko-atsume.emshea.com/cats', {}
        )
        .then((response) => {
          this.allCats = response.data
        }).catch((error) => {
          this.allCats = error.response.data
          console.log(error)
        })
    },
    getGoodies () {
      this.allGoodies = 'loading...'
      return axios
        .get('https://api.neko-atsume.emshea.com/goodies', {}
        )
        .then((response) => {
          this.allGoodies = response.data
        }).catch((error) => {
          this.allGoodies = error.response.data
          console.log(error)
        })
    },
    switchCatImg () {
      const newCatIndex = Math.floor(Math.random() * Math.floor(43))
      this.catImg = this.allCats[newCatIndex].CatImage
      this.catImgName = this.allCats[newCatIndex].CatName
      this.testInput = 'cats/' + (newCatIndex + 1)
      this.getTestResponse()
    }
  }
}

</script>

<style scoped>
.header-img {
  width: 40px;
}
:hover.header-img {
  cursor: pointer;
}
.cat-img {
  width: 40px;
}
.json {
  text-align: left;
}
.scrollbar-y {
  max-height: 212px;
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
  border: none;
  vertical-align: baseline;
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
@media(max-width:1000px){
  .input-group-desktop {
    visibility: hidden;
    display: none;
  }
  .input-group-mobile {
    visibility: visible;
    display: flex;
  }
}
</style>
