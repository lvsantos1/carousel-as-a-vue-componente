<template>
    <div id="carousel" :style="getCarouselTagInStyle()">
      <div id="catalog-items-container">         
        <div class="catalog-item" v-for='(ci,key) in catalog' v-bind:key="key" :class="(key == 0) ? 'active' : ''">
            <div class="src" :style="getDivSrcTagInStyle(ci.src)">
            </div>

            <div class="label" v-if="ci.label">
                {{ci.label}}
            </div>
        </div>
      </div>

      <div id="controls">
        <div class="prev arrow" v-on:click="prev()">❮</div>
        
        <div class="next arrow" v-on:click="next()">❯</div>
      </div>

      <div id="minis">
         <div class="mini" v-for='(ci,key) in catalog' v-bind:key="key" :class="(key == 0) ? 'active' : ''" v-on:click="goTo(key)">
            <img :src="ci.src" class="colorful">
            <img :src="ci.src" class="bnw">
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'Carousel',
  components: {
  },
  methods: {
    getDivSrcTagInStyle(image){
      let style = '';

      if(this.forceImageCover){
        style += 'background-size: cover; ';
      } else {
        style += 'background-size: contain; ';
      }

      style += 'background-image: url(' + image + ');';

      return style;
    },
    getCarouselTagInStyle() {
      let style = '';

      if(this.height) {
        style += 'height: ' + this.height + ';';
      }

      if(this.width) {
        style += ' width: ' + this.width + ';';
      }

      return style;
    },
    next(){
      let activatedMini = this.$el.querySelector('div#minis div.mini.active');
      let minisParentNode = activatedMini.parentNode;
      let activatedIndex = Array.prototype.indexOf.call(minisParentNode.children, activatedMini);

      if((activatedIndex + 1) == minisParentNode.children.length){
        this.goTo(0);
        return;
      }

      this.goTo(activatedIndex + 1);
    },
    prev(){
      let activatedMini = this.$el.querySelector('div#minis div.mini.active');
      let minisParentNode = activatedMini.parentNode;
      let activatedIndex = Array.prototype.indexOf.call(minisParentNode.children, activatedMini);

      if(activatedIndex == 0){
        this.goTo(minisParentNode.children.length - 1);
        return;
      }

      this.goTo(activatedIndex - 1);      
    },
    goTo(index) {
      let activatedMini = this.$el.querySelector('div#minis div.mini.active');
      let minisParentNode = activatedMini.parentNode;
      let miniToActive = minisParentNode.children[index];
      activatedMini.classList.remove("active");
      miniToActive.classList.add("active");

      let activatedCatalogItem = this.$el.querySelector('div#catalog-items-container div.catalog-item.active');
      let catalogItemsParentNode = activatedCatalogItem.parentNode;
      let catalogItemToActive = catalogItemsParentNode.children[index];
      activatedCatalogItem.classList.remove("active");
      catalogItemToActive.classList.add("active");
    }
  },
  props: {
    catalog: Array,
    height: String,
    width: String,
    forceImageCover: Boolean
  },
  data() {
    return {
    }
  }
}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100&display=swap');

  /* MAIN CONTAINER */
  
  div#carousel {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;

    position: relative;

    margin: 0 auto;
  }
  
  /* CATALOG ITEMS CONTAINER */

  div#catalog-items-container {
    display: block;
    height: 100%;
    width: 100%;
  }

  div#catalog-items-container div.catalog-item {
    display: none;
    height: 100%;
    width: 100%;

    position: relative;

    box-sizing: content-box;

    transition: opacity 0.15s linear;
    opacity: 0;
  }

  div#catalog-items-container div.catalog-item.active {
    display: block;
    opacity: 1;
  }

  div#catalog-items-container div.catalog-item div.src {
    display: block;
    height: 100%;
    width: 100%;


    background-repeat: no-repeat;
    background-position: center;
  }

  div#catalog-items-container div.catalog-item div.label {
    display: block;
    width: 100%;

    box-sizing: border-box;
    padding: 10px;

    position: absolute;
    top: 0;

    background: rgba(45,45,45,0.75);

    color: #c0c0c0;
    text-align: center;

    font: 400 16px 'Roboto', sans-serif;
  }

  /* CONTROLS: NEXT AND PREV */

  div#controls {
    display: flex;
    flex-direction: row;
    align-items: center;

    height: 50px;
    width: 100%;

    position: absolute;
    top: calc(50% - 25px);
  }

  div#controls div {
    font: normal 50px 'Roboto', sans-serif;
    color: #c0c0c0;
    line-height: 50px;

    padding: 5px;

    background: rgba(45,45,45,0.75);

    transition: color 0.15s linear;
  }

  div#controls div.next {
    position: absolute;
    right: 0;
  }

  div#controls div:hover {
    cursor: pointer;
    color: #f0f0f0;
  }

  /* MINIATURES */

  div#minis {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    height: 150px;
    width: 100%;

    box-sizing: border-box;
    padding: 10px 0px;

    position: absolute;
    bottom: 0px;
    
    background: rgba(45,45,45,0.75);
    opacity: 0;

    transition: opacity 0.15s linear;
    overflow-x: scroll;
    overflow-y: hidden;
  }

  div#minis div.mini {
    height: 100%;
    position: relative;
    border: 1px solid #333;
  }

  div#minis div.mini:first-child {
    margin-left: 10px;
  }

  div#minis div.mini:last-child {
    margin-right: 10px;
  }

  div#minis div.mini+div.mini {
    margin-left: 5px;
  }

  div#minis div.mini.active img.bnw {
    opacity: 0;
  }

  div#minis div.mini img {
    height: 100%;
  }

  div#minis div.mini img.colorful {
    position: absolute;
  }
  
  div#minis div.mini img.bnw {
    filter: grayscale(1);
    transition: opacity 0.3s linear;
  }

  /* WHEN MOUSEOVER */
  
  div#minis div.mini:hover img.bnw {
    opacity: 0;
    cursor: pointer
  }

  div#carousel:hover div#minis {
    opacity: 1;
  }

  /* MINIATURES SCROLLBAR */

  div#minis::-webkit-scrollbar {
    height: 25px;
  }

  div#minis::-webkit-scrollbar-track {
    background: transparent;
  }

  div#minis::-webkit-scrollbar-thumb {
    border: 7px solid rgba(0, 0, 0, 0);
    background-clip: padding-box;
    border-radius: 50px;
    background-color: #cacaca; 
  }
</style>