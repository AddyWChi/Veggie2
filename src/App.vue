<template>
  <div id="app">
    <header>
      <b-navbar toggleable="lg" type="dark" variant="info" fixed="top">
        <b-navbar-brand href="#">NavBar</b-navbar-brand>
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-navbar-nav class="ml-auto">
          <b-nav-item>
            {{ totalItemCount }}
          </b-nav-item>
        </b-navbar-nav>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <b-nav-item href="#">Link</b-nav-item>
            <b-nav-item href="#" disabled>Disabled</b-nav-item>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <b-nav-form>
              <b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
              <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
            </b-nav-form>

            <b-nav-item-dropdown text="Lang" right>
              <b-dropdown-item href="#">EN</b-dropdown-item>
              <b-dropdown-item href="#">ES</b-dropdown-item>
              <b-dropdown-item href="#">RU</b-dropdown-item>
              <b-dropdown-item href="#">FA</b-dropdown-item>
            </b-nav-item-dropdown>

            <b-nav-item-dropdown right>
              <!-- Using 'button-content' slot -->
              <template #button-content>
                <em>User</em>
              </template>
              <b-dropdown-item href="#">Profile</b-dropdown-item>
              <b-dropdown-item href="#">Sign Out</b-dropdown-item>
            </b-nav-item-dropdown>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </header>
    <ul>
      <li v-for="(m, errMsgCount) in errMsg" :key="errMsgCount++">
        {{ m }}
      </li>
    </ul>
    <OrderMenu :menu-items="menuItems" 
          @evt-err-invalid-prop="handleErrInvalidProp" 
          @evt-total-item-count="handleTotalItemCount" />
  </div>
</template>

<script>
import OrderMenu from './components/OrderMenu.vue'

export default {
  name: 'App',
  data() {
    return {
      // https://railsdrop.com/2025/11/07/browser-storage-mechanisms-explained-with-vue-js-examples/
      errMsg: [],
      errMsgCount: 0,
      menuItems: [-1, 20, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 100],
      items: [],
      totalItemCount: 0,
      payment: 0,
      adjustAmount: 0,
      adjustSign: true,  // Set true if it's a plus sign. Set false if it's a minus sign.
      changeAmount: 0,
    }
  },
  
  methods: {
    handleErrInvalidProp(msg) {
      console.error(`call handleErrInvalidProp: msg: ${msg}`);
      this.errMsg.push(msg);
    },
    handleTotalItemCount(count) {
      console.log(`call handleTotalItemCount: count: ${count}`);
      this.totalItemCount = count;
    }
  },

  components: {
    OrderMenu
  },

  beforeCreate() {
    console.log('call: App beforeCreate');
    return;
  },
  
  created() {
    console.log('call: App created');
    return;
  },

  beforeMount() {
    console.log('call: App beforeMount');
    return;
  },

  mounted() {
    console.log('call: App mounted');
    return;
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
