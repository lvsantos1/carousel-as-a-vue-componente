<template>
  <div id="mainContainer">
      <Carousel v-bind:catalog="catalog" v-bind:height="height" v-bind:width="width" v-bind:forceImageCover="forceImageCover"/>
  </div>
</template>

<script>
import Carousel from './Carousel.vue';

export default {
  name: 'App',
  components: {
    Carousel
  },
  methods: {
  },
  data() {
      return {
          catalog: [
              {
                  src: 'https://s2.glbimg.com/dUQlEe13EN9wsslG7FXLtqhSXB4=/smart/e.glbimg.com/og/ed/f/original/2020/04/22/montanhas-em-srvagen-noruega.jpg',
                  label: "Montanhas em Sørvågen, Noruega",
              },
              {
                  src: 'https://s2.glbimg.com/NfPqhyCL8PtjH3o9-46uLakI45k=/smart/e.glbimg.com/og/ed/f/original/2020/04/22/montanhas-em-srvagen-na-noruega.jpg',
                  label: "Cataratas do Athabasca em Alberta, Canadá",
              },
              {
                  src: 'https://s2.glbimg.com/gCUTC5DY0E7uLWsUrpJF7cK9XPo=/smart/e.glbimg.com/og/ed/f/original/2020/04/22/abraham-lake-em-alberta-canada.jpg',
                  label: "Abraham Lake, em Alberta, Canadá",
              },
              {
                  src: 'https://blog.emania.com.br/wp-content/uploads/2017/02/4.jpg',
                  label: "Paisagem aleatória",
              },
              {
                  src: 'https://www.estudokids.com.br/wp-content/uploads/2020/02/o-quee-e-paisagem-natural-grand-canyon.jpg',
                  label: "O Grand Canyon",
              },
              {
                  src: 'https://images.theconversation.com/files/125391/original/image-20160606-13080-s7o3qu.jpg?ixlib=rb-1.1.0&rect=273%2C0%2C2639%2C1379&q=45&auto=format&w=926&fit=clip',
              },
              {
                  src: 'https://previews.123rf.com/images/freeartist/freeartist1612/freeartist161200013/67472069-beautiful-mountain-landscapes-of-mauritius-island-with-famous-red-tree-.jpg',
              },
              {
                  src: 'https://fujifilm-x.com/wp-content/uploads/2019/09/Image-1.jpg',
              },
              {
                  src: 'https://www.diariesofmagazine.com/wp-content/uploads/2018/11/The-most-beautiful-landscapes-in-Kyrgyzstan_flowers.jpg',
              },
              {
                  src: 'https://www.telegraph.co.uk/content/dam/Travel/2018/December/oz-weird-mungo.jpg',
              },
              {
                  src: 'https://cdn.naturettl.com/wp-content/uploads/2019/10/28140244/ideas-for-photographing-winter-landscapes-14.jpg',
              },
          ],
          height: '100vh',
          width: '100%',
          forceImageCover: true,

      }
  }
}
</script>

<style>
    *,
    *:before,
    *:after {
        margin: 0;
        padding: 0;
    }

    div#mainContainer {
        display: block;
        width: 100%;
    }
</style>
