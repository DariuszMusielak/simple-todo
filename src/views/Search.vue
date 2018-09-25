<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input
        id="search"
        name="search"
        v-model="searchValue"
        @input="handleInput"
      />
    </div>
    <ul>
      <li v-for="item in results" :key="item.id">
        <p>{{ item.description }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'http://localhost:3000/api/v1';
export default {
  name: 'Search',
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      axios.get(`${API}/todos`)
        .then((response) => {
          this.results = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
  }

  .search {
    display: flex;
    flex-direction: column;
    width: 300px;

    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;
    }

    label {
      font-family: Montserrat, sans-serif;
    }
  }

</style>
