<template>
  <div class="hello">
    <enlargeImg :data="files"></enlargeImg>
  </div>
</template>

<script>
import enlargeImg from '../components/enlargeImg'
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      files:[
        {
          path:'http://img4q.duitang.com/uploads/item/201311/01/20131101141757_tunaj.png'
        },
        {
          path:'http://img5.duitang.com/uploads/item/201503/22/20150322122457_EQ3NP.thumb.700_0.jpeg'
        },
        {
          path:'http://tupian.enterdesk.com/uploadfile/2013/1219/20131219053302481.jpg'
        },
      ]
    }
  },
  components:{
    enlargeImg
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
