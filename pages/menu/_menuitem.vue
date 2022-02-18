<template>
  <div>
    <b-container>
      <h3>{{PageHeader}}</h3>
      <div>
        This will be replaced with better menu layout, just testing dynamic
        content pull
      </div>
      <NuxtLink to="/PrimaryMenu">Go back to Primary Menu</NuxtLink>
      <b-row>
        <b-col>
          <div v-for="item in C1items" :key="item.index">
          <div v-if="item.Header===1"><h5>{{ item.Text }}</h5></div>
          <div  v-if="item.Header===0">
         <div>{{ item.Text }}</div>
          <small v-if="item.Item">>> {{ item.Item }}</small>
          </div>
          </div>
        </b-col>
        <b-col v-if="col2">
          <div  v-for="item in C2items" :key="item.index">
          <div variant="primary" v-if="item.Header===1"><h5>{{ item.Text }}</h5></div>
          <div  v-if="item.Header===0">
         <div>{{ item.Text }}</div>
          <small v-if="item.Item">>> {{ item.Item }}</small>
          </div>
          </div>
        </b-col>
        <b-col v-if="col3">
          <div  v-for="item in C3items" :key="item.index">
          <div variant="primary" v-if="item.Header===1"><h5>{{ item.Text }}</h5></div>
          <div  v-if="item.Header===0">
         <div>{{ item.Text }}</div>
          <small v-if="item.Item">>> {{ item.Item }}</small>
          </div>
          </div>
        </b-col>
        <b-col v-if="col4">
          <div  v-for="item in C4items" :key="item.index">
          <div variant="primary" v-if="item.Header===1"><h5>{{ item.Text }}</h5></div>
          <div  v-if="item.Header===0">
         <div>{{ item.Text }}</div>
          <small v-if="item.Item">>> {{ item.Item }}</small>
          </div>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
//imports
import MenuData from '~/static/OrderMenus.json';
export default {

  async asyncData({ params, redirect }) {
    const filteredMenuItem = MenuData.find(
      (el) => el.Name.replace(/\W/g, '_') === params.menuitem
    );
    if (filteredMenuItem) {
      let C1items = filteredMenuItem.contents
        .filter((i) => i.Column === 1)
        .sort((x, y) => x.Row - y.Row);
      let C2items = filteredMenuItem.contents
        .filter((i) => i.Column === 2)
        .sort((x, y) => x.Row - y.Row);
      let C3items = filteredMenuItem.contents
        .filter((i) => i.Column === 3)
        .sort((x, y) => x.Row - y.Row);
      let C4items = filteredMenuItem.contents
        .filter((i) => i.Column === 4)
        .sort((x, y) => x.Row - y.Row);
      let col1 = C1items.length > 0;
      let col2 = C2items.length > 0;
      let col3 = C3items.length > 0;
      let col4 = C4items.length > 0;
      return {
        C1items,
        C2items,
        C3items,
        C4items,
        col1,
        col2,
        col3,
        col4,
        PageHeader: filteredMenuItem.Name
      };
    } else {
      return { items: [] };
      redirect('/');
    }
  },
};
</script>

<style></style>
