<template>
  <div>
     
    <b-row>
      <b-col xl="3" offset-xl="1">
        <img src="src/logo.png" id="logo" />
      </b-col>
    </b-row>
    <b-row xl="2" offset-xl="6">
      <b-col xl="3" offset-xl="8">
        <input type="text" value="Search Title..." v-model="search" />
      </b-col>
    </b-row>

    <b-row>
      <div v-for=" (row,idx) in filter" v-bind:key="idx">
        <b-col xl="11" offset-xl="1">
          <vue-flip :active-hover="true" width="600px" height="400px" class="simple-test" id="flip">
            <div slot="front">
              <img v-bind:src="`${row.cover}`" id="img1" />
            </div>
            <div slot="back">
              {{row.title}}
              <br />
              {{row.description}}
              <br />
              {{row.language}}
              <br />
              <button @click="showimg(row.detail,row.cover)" id="button">Detail</button>
              <vue-easy-lightbox :visible="visible" :imgs="imgs" @hide="handleHide"></vue-easy-lightbox>
            </div>
          </vue-flip>
        </b-col>
      </div>
    </b-row>
  </div>
</template>


<script>
import VueFlip from "vue-flip";
import Vue from "vue";
import Lightbox from "vue-easy-lightbox";
import VueEasyLightbox from "vue-easy-lightbox";
Vue.use(Lightbox);

export default {
  props: ["rows"],
  name: "UserList",
  data() {
    return {
      isLoading: true,
      search: "",
      imgs: "", // Img Url ,
      
      visible: false,
      index: 0 // defaul
    };
  },
  
  methods: {
    showimg(url1,url2) {
      this.imgs = [url1,url2],
       this.index=1,
       this.show();
        
    },
    show() {
      this.visible = true;
    },
    handleHide() {
      this.visible = false;
    }
  },
  computed: {
    filter: function() {
      let booktitle = this.rows.filter(book => {
        return (
          book.title.toLowerCase().includes(this.search.toLowerCase()) ||
          this.search == ""
        );
      });
      console.log(booktitle);
      return booktitle;
    }
  },
  components: {
    "vue-flip": VueFlip,
    VueEasyLightbox
  }
};
</script>
<style>
.front {
  display: flex;
  align-items: center;
  /* justify-content: center; */
  background-color: #673ab7;
  color: white;
}

.back {
  display: flex;
  align-items: center;
  /* justify-content: center; */
  background-color: #ffc107;
  color: white;
}
#flip {
  margin-bottom: 40px;
}
#img1 {
  width: 600px;
  height: 400px;
}

#detail {
  width: 600px;
  height: 400px;
}
input{
    margin-bottom: 10px;
    width: 250px;
    border-color: rgb(10, 10, 36)
}
</style>