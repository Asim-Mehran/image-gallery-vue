<template>
  <div id="imagegallery">
    <div class="row mb-2 d-flex align-items-center justify-content-center">
      <div class="col-xl-3 col-lg-4 col-sm-6 col-md-6 ml-2">
        <input
          v-model="searchKeyword"
          @keyup="onTypeSearch()"
          type="text"
          placeholder="Type to search"
          class="search form-control"
        />
      </div>
    </div>
    <div class="row mb-2 d-flex align-items-center justify-content-center">
      <div class="card w-75" style="width: 60rem">
        <div class="card-body">
          <div class="row mt-5" v-if="isLoading">
            <div class="text-center">
              <b-spinner variant="primary" label=""></b-spinner>
            </div>
            <div class="text-center">Loading...</div>
          </div>

          <div v-if="!isLoading" class="row" style="position: relative">
            <img
              v-bind:key="image.id"
              v-for="image in filterList"
              class="img-thumbnail w-auto h-100 img-fluid"
              alt="Responsive image"
              v-bind:src="getRandomSizeUrl(image.url)"
              style="position: relative"
              v-b-tooltip.hover
              @click="onClickImage(image)"
              :title="image.title"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
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
      imageRandomSizeLimit: 50,
      imageRandomSizeOffset: 100,
      apiImageLimit: 16,
    };
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  position: relative;
}

.image {
  display: block;
  width: auto;
  height: auto;
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

.container:hover .overlay {
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
</style>
