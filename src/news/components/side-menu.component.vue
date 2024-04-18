<script>
import {NewsApiService} from "../services/news-api.service.js";
import PvSidebar from "../../main.js";
import PvAvatar from "../../main.js";

export default {
  name: "side-menu",
  components: {PvAvatar, PvSidebar},
  props:{
    visible: Boolean
  },
  data(){
    return{
      sources: [],
      errors: [],
      newsApi: NewsApiService()
    }
  },
  created(){
    this.newsApi.getSources()
        .then(response =>{
          this.sources = response.data.sources;
          this.sources.forEach(source =>{
            source.urlToLogo = this.newsApi.getUrlToLogo(source); // IN HERE WE ADD A NEW PROPERTY CALLED "urlToLogo"
            console.log(`data: ${response.data.sources}`);
          })
        })
        .catch(e=> this.errors.push(e));
  },
  methods:{
    onSourceSelected(source){
      this.$emit('source-selected', source);
    },

    isVisible(){
      return this.visible;
    }
  }
}
</script>

<template>
  <pv-sidebar v-bind:visible="visible" >
    <div v-for="source in sources" class="m-4">
        <div class="flex align-content-start flex-wrap"> <!-- flex-wrap means: Specify if the elements are in the same line -->
            <span class="flex align-items-center justify-content-center mr-2">
              <pv-avatar :aria-label="source.name" :image="source.urlToLogo" shape="circle"/>
            </span>

            <span class="flex align-items-center justify-content-center">
                {{source.name}}
            </span>
        </div>
    </div>
  </pv-sidebar>
</template>