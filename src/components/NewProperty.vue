<template>
  <div class="property-form">
    <h3>New Property</h3>
    <form>
      <div class="form-group">
        <label for="propName">Property name</label>
        <input type="text" class="form-control" id="propName" placeholder="Enter property name">
      </div>
      <div class="form-group">
        <label for="propAddress">Property address</label>
        <!--<input type="text" class="form-control" id="propAddress" placeholder="Enter address of property">-->
        <textarea class="form-control" id="propAddress" rows="2"></textarea>
      </div>
      <div class="form-group">
        <label for="propCity">Property city</label>
        <input type="text" class="form-control" id="propCity" placeholder="Enter city of property">
      </div>
      <button class="btn-primary" style="margin-top: 10px" >Submit</button>
    </form>
  </div>
</template>

<script>

export default {
  name: 'NewProperty',
//  components: {
//    TreeMap,
//    bar_chart: BarChart,
//    bootstrap_table: BootstrapTable
//  },
  computed: {
//    barData() {
//      console.log(this.$store.getters)
//      return this.$store.getters.treeData
//    }
  },
  data () {
    return {
      propertyList: null
    }
  },
  mounted () {
    var me = this;
    console.log(this.uData)
    let url = 'http://167.99.14.10/properties'
    this.$http.get(url).then(response => {
      me.propertyList = response.data
      console.log(response.data)
    })

  },
  methods: {
    parseDate (d) {
      let y = new Date(d.substring(0, 4),
        d.substring(5, 7),
        d.substring(8, 10))
      return y;
    },
    viewPropertyFloorplans(pid) {
      let url = 'property/' + pid.toString()
      this.$router.push(url)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.property-form {
  width: 40%;
  position: relative;
  left: 30%;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
