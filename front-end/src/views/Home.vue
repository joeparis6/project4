<template>
<div class="home">
  <h1>Basketball Players</h1>
  <section class="image-gallery">
    <div class="image" v-for="item in items" :key="item.id">
      <h1>{{item.player}}</h1>
      <p>{{item.college}}</p>

      <img :src="item.path" />
    </div>
  </section>

  <footer>
    
  </footer>
</div>

</template>

<script>
// @ is an alias to /src
import axios from 'axios';

export default {
  name: 'Home',
  data() {
  return {
   items: [],
  }
},
created() {
  this.getItems();
},
methods: {
  async getItems() {
    try {
      let response = await axios.get("/api/items");
      this.items = response.data;
      return true;
    } catch (error) {
      // error
    }
  },
}

}
</script>

<style scoped>

.home {
  background: #2222ed;
  text-align: center;
  color: white;
}

.image-gallery {
  color: white;
}


.image h2 {
  font-style: italic;
}

/* Masonry */
*,
*:before,
*:after {
  box-sizing: inherit;
}

.image-gallery {
  column-gap: 1.5em;
}

.image {
  margin: 0 0 1.5em;
  display: inline-block;
  width: 100%;
}

.image img {
  width: 100%;
}

/* Masonry on large screens */
@media only screen and (min-width: 1024px) {
  .image-gallery {
    column-count: 4;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .image-gallery {
    column-count: 3;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .image-gallery {
    column-count: 2;
  }
}
</style>
