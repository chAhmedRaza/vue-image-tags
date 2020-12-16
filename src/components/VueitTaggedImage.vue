<template>
  <div class="hello">    
    <div class="image-container">
               
        <vueit-popover v-for="(tag, index) in tags" :isOpen="tag.isOpen" @trigger-popover="tag.isOpen = !tag.isOpen" :key="index" :style="{position: 'absolute', top: tag.yPercentage + '%', left: tag.xPercentage + '%'}">
          <template v-slot:popoverButton>
            <div class="tag-outer-circle" :style="{border: '1px solid' + markerColor}">
                <div class="tag-inner-circle" :style="{background: markerColor}"></div>
            </div>
          </template>

          <template v-slot:popoverContent>
              <div class="popover-content">
                <a :href="tag.link" :target="linkTarget" class="link" >
                  <img src="@/assets/link.png" />
                </a>
                <h4>{{ tag.title }}</h4>
                <small>{{ tag.description }}</small>
              </div>
          </template>
      </vueit-popover>
       
      <img :src="src" ref="image" style="width: 100%; border: 1px solid black;" alt="bicycle">

        
    </div>
    
  </div>
</template>

<script>

import VueitPopover from "./VueitPopover.vue";

export default {
  name: 'VueitTaggedImage',
  components: { VueitPopover },
  props: {
      tags: {
        type: Array,
        required: true
      },
      src: {
        type: String,
        required: true
      },
      markerColor: {
        type: String,
        default: '#26abff'
      },
      linkTarget: {
        type: String,
        default: '_self'
      }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.image-container{
    position: relative;
}
h3 {
  margin: 40px 0 0;
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

.tag-outer-circle{
    cursor: pointer;
    padding: 5px;
    height: 20px;
    width: 20px;
    border-radius: 100px;
    /* border: 1px solid red; */
    transform: translate(-15px, -15px);
}

.tag-inner-circle{
    height: 20px;
    width: 20px;
    border-radius: 100px;
    /* background: red; */
}

.popover-content{
  text-align: left;
  min-width: 100px; 
}

.popover-content *{
  margin: 0;
}

.link{
  float: right;
}

.link img{
  height: 15px;
}
</style>
