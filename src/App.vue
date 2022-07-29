<template>
  <div id="app">
    <nav>
      <router-link to="/">Image Gallery</router-link>
    </nav>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<!-- 

<template>
  <div class="card w-75">
    <packing-grid
      class="container"
      v-bind:gap="gap"
      v-bind:defaultDirection="defaultDirection"
      v-bind:sizeWeight="sizeWeight"
      v-bind:ratioWeight="ratioWeight"
      v-bind:weightPriority="weightPriority"
      v-bind:aspectRatio="aspectRatio"
    >
      <div class="item">
        <img
          v-bind:key="image.id"
          v-for="image in filterList"
          class="img-thumbnail w-auto h-auto img-fluid"
          alt="Responsive image"
          v-bind:src="getRandomSizeUrl(image.url)"
        />
      </div>
    </packing-grid>
  </div>
</template>

<script>
import { PackingGrid } from "@egjs/vue-grid";

export default {
  name: "ImageGallery",
  data() {
    return {
      imageList: [],
      sizes: [],
      filterList: [],
      searchKeyword: "",
      isLoading: false,
      displayRandomImageSizeCount: 4,
      imageRandomSizeLimit: 100,
      imageRandomSizeOffset: 100,
      apiImageLimit: 16,
      gap: 5,
      defaultDirection: "end",
      sizeWeight: 1,
      ratioWeight: 1,
      aspectRatio: 1,
      weightPriority: "custom",
    };
  },
  components: {
    PackingGrid,
  },
  methods: {
    onClickImage: function (image) {
      this.$router.push({ name: "imagedetail", params: { image } });
    },
    onTypeSearch: function () {
      this.filterList = this.imageList.filter((x) =>
        x.title.toLowerCase().includes(this.searchKeyword.trim().toLowerCase())
      );
    },
    getRandomNumber: (limit, offset) => {
      return Math.floor(Math.random() * limit) + (offset > 0 ? offset : 0);
    },
    getRandomSizeUrl: function (url) {
      let splitUrl = url.split("600");
      let number = this.getRandomNumber(this.displayRandomImageSizeCount);
      return `${splitUrl[0]}/${this.sizes[number]}/${splitUrl[1]}`;
    },
    setRandomSizesArray: function () {
      for (let index = 0; index < this.displayRandomImageSizeCount; index++) {
        this.sizes.push(
          this.getRandomNumber(
            this.imageRandomSizeLimit,
            this.imageRandomSizeOffset
          )
        );
      }
    },
  },
  created: function () {
    this.isLoading = true;
    this.setRandomSizesArray();
    (async () => {
      try {
        const response = await this.axios.get(
          "https://jsonplaceholder.typicode.com/photos"
        );
        if (response) {
          this.imageList = response.data.slice(0, this.apiImageLimit);
          this.filterList = response.data.slice(0, this.apiImageLimit);
        }
      } catch (error) {
        alert(error);
      }
      this.isLoading = false;
    })();
  },
};
</script>

 <style scoped>
html,
body {
  position: relative;
  height: 100%;
  padding: 0 !important;
  margin: 0 !important;
}
.container {
  overflow: hidden;
}
.containe-roverlay {
  position: relative;
}

.image {
  position: relative;
  width: 100%;
  font-size: 0;
}
.image img {
  width: 100%;
}
.item {
  position: absolute;
  /* border: 1px solid #ccc; */
  text-align: center;
}
.search::-ms-clear {
  display: none;
}

.overlay {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  height: 100%;
  width: 100%;
  opacity: 0;
  transition: 0.5s ease;
  background-color: #008cba;
}

.container-roverlay:hover .overlay {
  opacity: 1;
}

.text {
  color: white;
  font-size: 20px;
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  text-align: center;
}
</style> -->
