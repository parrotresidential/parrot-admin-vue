<template>
  <div class="hello">
    <h3>Properties</h3>
    <div v-if="propertyList">
      <div v-for="p in propertyList" class="property-card card" v-on:click="viewPropertyFloorplans(p.id)">
        <div class="property-name">
          {{ p.name }} - {{ p.floorplans.length }} floorplans
        </div>
        <div class="property-info">
          {{ p.address }}
        </div>
      </div>
    </div>
    <button class="btn-primary" style="margin-top: 50px" v-on:click="newProp=true" v-if="!newProp">Add new</button>
    <property_form v-if="newProp"></property_form>
  </div>
</template>

<script>
import PropertyForm from './NewProperty.vue'
export default {
  name: 'PropertyList',
  components: {
    property_form: PropertyForm
  },
  computed: {
  },
  data () {
    return {
      newProp: false,
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
