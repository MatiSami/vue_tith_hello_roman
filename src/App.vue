<template>
   <div class="wrapper">
    <Claim />
    <SearchInput v-model="searchValue" @input="handleInput"/>
    <HeroImage/>
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue'
import SearchInput from '@/components/SearchInput.vue'
import HeroImage from '@/components/HeroImage.vue'

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    HeroImage
  },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;800&display=swap');

  * {
    box-sizing: border-box;
  }

  body {
    font-family: 'Montserrat', sans-serif;
    margin: 0;
    padding: 0;
  }

  .wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  min-height: 100vh;
  height: 100vh;
  justify-content: center;
}

</style>
