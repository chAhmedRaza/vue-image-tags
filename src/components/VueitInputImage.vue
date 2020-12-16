<template>
  <div class="hello">
    <div class="image-container">
      <vueit-popover class="current-tag" :isOpen="true" v-if="showCurrentTag" :style="{ position: 'absolute', top: newYPercentage + '%', left: newXPercentage + '%' }">
        <template v-slot:popoverButton>
          <div class="tag-outer-circle" @click="showCurrentTag = !showCurrentTag">
              <div class="tag-inner-circle"></div>
          </div>
        </template>

        <template v-slot:popoverContent>
              <input class="vueit-popover-input" name="title" placeholder="Title" type="text" v-model="newTitle" /> 
              <br>
              <input class="vueit-popover-input" name="description" placeholder="Description" type="text" v-model="newDescription" />
              <br>
              <input class="vueit-popover-input" name="link" placeholder="URL" type="text" v-model="newLink" />
              <br>
              <input type="hidden" v-model="newXPercentage" />
              <input type="hidden" v-model="newYPercentage" />
              <a @click="showCurrentTag = false" class="remove-tag-button">
                  <small>Cancel</small>
                </a>
              <button class="vueit-popover-button" @click="addTag">Apply</button>
        </template>
      </vueit-popover>

      <vueit-popover v-for="(tag, index) in tags" :isOpen="tag.isOpen" @trigger-popover="tag.isOpen = !tag.isOpen" :key="index" :style="{position: 'absolute', top: tag.yPercentage + '%', left: tag.xPercentage + '%'}">
          <template v-slot:popoverButton>
            <div class="tag-outer-circle" :style="{border: '1px solid' + markerColor}">
                <div class="tag-inner-circle" :style="{background: markerColor}"></div>
            </div>
          </template>

          <template v-slot:popoverContent>
              <form>
                <input class="vueit-popover-input" name="title" placeholder="Title" type="text" v-model="tag.title" /> 
                <br>
                <input class="vueit-popover-input" name="description" placeholder="Description" type="text" v-model="tag.description" />
                <br>
                <input class="vueit-popover-input" name="link" placeholder="URL" type="text" v-model="tag.link" />
                <br>
                <input type="hidden" v-model="newXPercentage" />
                <input type="hidden" v-model="newYPercentage" />

                <a @click="removeTag(index)" class="remove-tag-button">
                  <small>Remove</small>
                </a>
              </form>
          </template>
      </vueit-popover>

      <img :src="src" class="tag-image" ref="image" style="width: 100%; border: 1px solid black;" @click="setCurrentTagCoordinates" alt="bicycle">
    </div>
  </div>
</template>

<script>

import VueitPopover from './VueitPopover.vue';

export default {
  name: 'VueitInputImage',
  components: { VueitPopover },
  data(){
    return{
      showCurrentTag: false,
      showTitleInput: false,
      newXPercentage: '',
      newYPercentage: '',
      newTitle: '',
      newDescription: '',
      newLink: '',
      tags: [],
    }
  },
  
  props: {
    src: {
      type: String,
      required: true
    },
    markerColor: {
      type: String,
      default: '#26abff'
    }
  },

  methods: {
    setCurrentTagCoordinates(event){
      this.newXPercentage = event.offsetX / this.$refs.image.clientWidth * 100;
      this.newYPercentage = event.offsetY / this.$refs.image.clientHeight * 100;
      this.showTitleInput = true;
      this.showCurrentTag = true;
    },
    addTag(){
      this.tags.push({ title: this.newTitle, description: this.newDescription, link: this.newLink, xPercentage: this.newXPercentage, yPercentage: this.newYPercentage, isOpen: false });
      this.showTitleInput = false;
      this.showCurrentTag = false;
      this.newTitle = '';
      this.newXPercentage = '';
      this.newYPercentage = '';
      this.newDescription = '';
      this.newLink = '';
      

      this.$emit('modify', this.tags);
    },
    removeTag(index){
      this.tags.splice(index, 1);
    }


  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tag-image:hover{
  cursor: crosshair;
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
  color: #9daaa4;
}

.image-container{
    position: relative;
}

.tag-outer-circle{
    cursor: pointer;
    padding: 5px;
    height: 20px;
    width: 20px;
    border-radius: 100px;
    border: 1px solid red;
    transform: translate(-15px, -15px);
}

.tag-inner-circle{
    height: 20px;
    width: 20px;
    border-radius: 100px;
    background: red;
}

.current-tag .tag-outer-circle{
    border: 1px solid #666666;
}

.current-tag  .tag-outer-circle .tag-inner-circle{
    background: #666666;
}

.vueit-popover-input{
  padding: 10px;
  border: 1px solid lightgrey;
  border-radius: 5px;
  margin-bottom: 10px;
}

.vueit-popover-button{
  padding: 5px 15px;
  border-radius: 5px;
  cursor: pointer;
  background: #26abff;
  color: white; 
  float: right;
  border: 1px solid transparent;
}

.remove-tag-button{
  color: red;
  float: left;
  cursor: pointer;
}
</style>
