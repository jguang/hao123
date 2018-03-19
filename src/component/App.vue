<template>
  <div class="app">
      <nav-list :data="navListData" @selected="selectedEvent"></nav-list>
      <nav-links :current-book-marks="currentBookMarks"></nav-links>
  </div>
</template>
<style lang="less">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    list-style: none;
}
html,
body {
    background: #f1f1f1;
    font-family: Roboto, 'Helvetica Neue', Arial, sans-serif;
    background: url(http://api.dujin.org/bing/1366.php) 0 0 no-repeat;
    background-size: cover;
    font-size: 14px;
    height: 100%;
    overflow: hidden;
}
</style>

<script>
const bookData = require('../../bookmarks/*');
import NavLinks from './NavLinks';
import NavList from './NavList';
export default {
    data() {
        return {
            initData: bookData,
            selected: null
        };
    },
    computed: {
        navListData() {
            return Object.keys(this.initData);
        },
        currentBookMarks() {
            return this.initData[this.selected];
        }
    },
    mounted() {},
    methods: {
        selectedEvent(key) {
            this.selected = key;
        }
    },
    components: {
        NavList,
        NavLinks
    }
};
</script>
