<template>
    <div id="docs">
        <div class="row pt-5 pb-1">
            <div class="col">
                <h4>Documentation</h4>
            </div>
        </div>
        <div class="row">
            <div class="col docs-subheader">
                <h5>Overview</h5>
                <p>Use this API to get data on cats and goodies from Neko Atsume: Kitty Collector.</p>
                <p>This API is rate limited at 100 API requests per minute. Please feel free to <a href="mailto:neko@emshea.com">reach out</a> with questions.</p>
            </div>
        </div>
        <hr>
        <div class="row">
          <div class="col docs-subheader">
              <h5>Cats</h5>
              <p>Return data for cats from the game. There is an endpoint for all goodies and an endpoint that returns goodies by id or by name. Valid ids are between 1-66. Names are not case sensitive. See <a href="https://nekoatsume.fandom.com/wiki/Cats">Neko Atsume wiki</a> for more info on cats.</p>
              <h6> GET /cats </h6>
              <div class="row json">
                  <div class="col scrollbar-y border mx-3 mb-3">
                      <tree-view :data="cats" :options="{maxDepth: 3}"></tree-view>
                  </div>
              </div>
              <h6>GET /cats/{id or name}</h6>
              <div class="row json">
                  <div class="col scrollbar-y border mx-3">
                      <tree-view :data="catExample" :options="{maxDepth: 3}"></tree-view>
                  </div>
              </div>
              <div class="row table-row py-3">
                <div class="col table-col">
                  <table class="table table-responsive-md table-bordered">
                    <thead>
                        <tr>
                          <th scope="col">Name</th>
                          <th scope="col">Description</th>
                          <th scope="col">Example</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in catData" :key="item.Id">
                          <td>{{ item.Name }}</td>
                          <td>{{ item.Description }}</td>
                          <td>{{ item.Example }}</td>
                        </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
        </div>
        <hr>
        <div class="row">
          <div class="col docs-subheader">
              <h5>Goodies</h5>
              <p>Returns data for goodies. There is an endpoint for all goodies and an endpoint that returns goodies by id or by name. Valid ids are between 1-66. Names are not case sensitive. See <a href="https://nekoatsume.fandom.com/wiki/Goodies">Neko Atsume wiki</a> for more info on goodies.</p>
              <h6>GET /goodies </h6>
              <div class="row json">
                  <div class="col scrollbar-y border mx-3 mb-3">
                      <tree-view :data="allGoodies" :options="{maxDepth: 3}"></tree-view>
                  </div>
              </div>
              <h6>GET /goodies/{id or name}</h6>
              <div class="row json">
                  <div class="col scrollbar-y border mx-3">
                      <tree-view :data="goodieExample" :options="{maxDepth: 3}"></tree-view>
                  </div>
              </div>
              <div class="row table-row py-3">
                <div class="col table-col">
                  <table class="table table-responsive-md table-bordered">
                    <thead>
                      <tr>
                        <th scope="col">Name</th>
                        <th scope="col">Description</th>
                        <th scope="col">Example</th>
                      </tr>
                    </thead>
                    <tbody>
                      <tr v-for="item in catData" :key="item.Id">
                        <td>{{ item.Name }}</td>
                        <td>{{ item.Description }}</td>
                        <td>{{ item.Example }}</td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'docs',
  props: ['cats'],
  data () {
    return {
      catExample: { CatId: '1', CatName: 'Snowball', CatImage: 'https://neko-atsume.s3.amazonaws.com/img/Snowball.jpg', MementoImage: 'https://neko-atsume.s3.amazonaws.com/img/Flowered+Collar.jpg', CatDescription: 'Solid White', CatPersonality: 'Mellow', CatPowerLevel: '80', Memento: 'Flowered Collar', CatType: 'Common' },
      goodieExample: 'example goodie response',
      allGoodies: 'data for all goodies',
      catData: [
        { Name: 'CatId', Description: 'Id number of cat (1-66)', Example: '1', Id: '1' },
        { Name: 'CatName', Description: 'Name of the cat', Example: 'Snowball', Id: '2' },
        { Name: 'CatDescription', Description: 'Description of cat appearance', Example: 'Solid White', Id: '3' },
        { Name: 'CatPersonality', Description: 'Description of cat personality characteristics', Example: 'Mellow', Id: '4' },
        { Name: 'CatPowerLevel', Description: 'Power level of cat', Example: '80', Id: '5' },
        { Name: 'Memento', Description: 'Memento item left by cat', Example: 'Flowered Collar', Id: '6' },
        { Name: 'CatType', Description: 'Type of cat (rare or common)', Example: 'Common', Id: '7' },
        { Name: 'CatImage', Description: 'Link to cat image file', Example: 'https://neko-atsume.s3.amazonaws.com/img/Snowball.jpg', Id: '8' },
        { Name: 'MementoImage', Description: 'Link to memento image file', Example: 'https://neko-atsume.s3.amazonaws.com/img/Flowered+Collar.jpg', Id: '9' }
      ]
    }
  },
  mounted () {

  },
  methods: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.docs-subheader {
  text-align: left;
}
.scrollbar-y {
  max-height: 212px;
  overflow-y: auto;
}
.row .table {
  width: unset;
}
@media(max-width:767px){
  .table {
    font-size: 13px;
  }
}
</style>
