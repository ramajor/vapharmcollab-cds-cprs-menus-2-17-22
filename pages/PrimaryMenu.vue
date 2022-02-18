<template>
  <div>
    <h3>Primary Menus (after site selection)</h3>
    <NuxtLink to="/">Home page</NuxtLink>
    <ul>
      <li v-for="item in items" :key="item.index">
        <a :href="item.link">
          {{ item.title }}
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
//imports
name = 'PrimaryMenu';
import MenuData from '~/static/OrderMenus.json';
export default {
  data: function () {
    return {
      items: [],
    };
  },
  created() {
    this.items = MenuData.map(GetMenuTitles);
    function GetMenuTitles(item) {
      let link = '/menu/' + item.Name.replace(/\W/g, '_');
      return { title: item.Name, link: link };
    }
  },
};
</script>

<style></style>
