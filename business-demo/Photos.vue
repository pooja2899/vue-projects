<template>
  <div>
    <v-app class="ma-0 pa-0">
      <Search
        :title="$t('photos')"
        @search-data="updateSearchData"
      />
      <Sidebar
        v-bind:categories="categories"
        @category="updateCatData"
      />
      <div class="container mt-6">      
        <div class="column is-5">
        <p class="mt-6 mb-6">
        </p> 
        <p class="mt-6 mb-6">
        </p>    
        <p class="mb-6">
        </p>   
        <p class="mb-6">
        </p>  
        <form ref="form" enctype="multipart/form-data" @submit.prevent="upload">                                              
          <image-uploader
            :id="fileInput"
            :debug="1"
            :maxWidth="512"
            :quality="0.7"
            :autoRotate=true
            outputFormat="verbose"
            :preview=true
            :className="['fileInput', { 'fileInput--loaded' : hasImage }]"
            :capture="false"
            accept="video/*,image/*"
            doNotResize="['gif', 'svg']"
            @input="setImage"
            @onUpload="startImageResize"
            @onComplete="endImageResize">
              <label for="fileInput" slot="upload-label">
                    <span class="icon is-small m-2">
                      <i class="fas fa-camera fa-lg"></i>
                    </span>
                <span class="upload-caption">{{ hasImage ? 'Replace' : 'Upload' }}</span>
              </label>
            </image-uploader>
            <div class="control">
                <button v-on:click="upload(this.fileInput)" class="button is-link">{{$t('upload')}}</button>
            </div>         
        </form>
      </div>
      <div class="row" v-for="key in 4" v-bind:key="key">
        <div class="column" v-for="key in 4" v-bind:key="key">
            <div class="card">
              <div class="card-image">
                <figure class="image is-4by3">
                  <img src="https://bulma.io/images/placeholders/1280x960.png" alt="Placeholder image">
                </figure>
              </div>
            </div>
          </div>
        </div>
      </div>
    </v-app> 
  </div>
</template>
<script>
import Search from "@/components/Search.vue";
import Sidebar from "@/components/Sidebar.vue";
import ImageUploader from 'vue-image-upload-resize'
import json from "@/views/photos/categories.json";
import axios from "axios";

export default {
  name: "Result",
  components: {
    Search,
    Sidebar,
    ImageUploader
  },
  props: [],
  data() {
    return {
      data: null,
      categories:json
    };
  },
  methods: {
    updateSearchData(data) {
      this.data = null;
      this.data = data;
    },
    updateCatData(data) {
      console.log(data)
      this.data = [];
      this.data = data;
    },
    setImage (file) {
      this.hasImage = true
      this.image = file
    },
    startImageResize (file) {
      this.hasImage = true
      this.image = file
    },       
    endImageResize (file) {
      this.hasImage = true
      this.image = file
    },
    upload(file){
      const url = this.$store.state.base_url + "upload";
      console.log("uploading file..", file)
      axios
        .post(url, file)
        .then((res) => {
          this.status = res;
        })
        .catch((error) => { 
          console.error(error);
        });
    },        
  },
  created() {
  },  
};
</script>

<style>
  .page-margin{
    margin-top: 105px;
  }
</style>