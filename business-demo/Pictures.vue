<template>
    <div class="card has-background-link-light mt-2">
      <div class="level is-mobile p-0 m-1">
        <div class="level-left">
            <span class="card-header-title p-1 m-0">{{$t('in-the-news')}}</span>
        </div>
        <div class="level-right">
            <span class="icon is-small m-2">
                <i class="fas fa-camera fa-sm"></i>
            </span>
        </div>
        </div> 
        <div class="card-content p-2 m-0">
            <div class="columns is-multiline">
                <div v-for="pic in pictures" v-bind:key="pic" class="column is-one-third p-2 m-0">
                  <div class="hover01">
                    <figure class="image is-square">
                        <a target="_blank" v-bind:href="JSON.parse(pic).article_url">
                          <img 
                              v-if="JSON.parse(pic).image_url"
                              :src="imgUrl(JSON.parse(pic).image_url)"   
                              :title="JSON.parse(pic).website"                         
                          />      
                        </a>          
                    </figure>
                  </div>
                </div>
            </div>
        </div>
    </div>            
</template>

<script>
import axios from "axios";
export default {
  name: "Pictures",
  data() {
    return {
      query :null,
      pictures: null
    };
  },
  methods: {
    imgUrl(url) {
        var imageurl; 
        const regex = "(//(?:.*?)(?:jpg|jpeg|png))";
        var matches = url.matchAll(regex);
        for (const m of matches) {
          var value =  m[0];
          if (value !=null){
            imageurl = 'http:'+value;
            break;
          }
        }
        return imageurl;        
    },        
    getPictures() {
      const url = this.$store.state.base_url + "pictures";
      const params = new URLSearchParams();
      params.append('q', this.query);         
      axios
        .get(url, {params: params})
        .then((res) => {
          this.pictures = res.data.pictures.filter(el => el.image_url !== null).slice(0,9);
          //console.log("pictures" , this.pictures)
        })
        .catch((error) => {
          console.error(error);
        });
    },    
  },
  watch: {
    $route(value) {
      if(value.query.q){  //from search bar
        this.query = value.query.q;
      }else if (value.query.c){ //if category
        this.query = value.query.c;
      }
      this.getPictures();
    },     
  },   
  created() {
    if (this.$route.query.q){ //if query
      this.query = this.$route.query.q;
    }else { //default
      this.query = "None";
    }
    this.getPictures();
  }      
};
</script>

<style scoped>
  .hover01 figure a img {
    -webkit-transform: scale(1);
    transform: scale(1);
    -webkit-transition: .3s ease-in-out;
    transition: .3s ease-in-out;
  }
  .hover01 figure:hover a img {
    -webkit-transform: scale(1.3);
    transform: scale(1.3);
  }
</style>