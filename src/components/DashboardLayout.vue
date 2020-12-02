<template>
  <div>
    <b-button v-b-toggle.sidebar-backdrop width="500px" id="listHam"><b-icon icon="list"></b-icon></b-button>
    <b-sidebar id="sidebar-backdrop" aria-labelledby="sidebar-no-header-title" no-header backdrop-variant="transparent" backdrop shadow>
      <template #default="{ hide }">
        <div class="p-3" id="sidebar">
            <img src="../assets/logo-reversed.png" width="50" height="50">
            
          <br><br><br><br>

          <nav class="mb-1" id="DatMas">
              <b-nav-item href="/account" @click="hide">
                <div id="warnaDL">
                  <b-icon icon="person-fill"></b-icon>
                    <span style="color: #151D65;">______</span>Account
                  </div>
              </b-nav-item><br><br>
              <b-nav-item href="/products" @click="hide">
                <div id="warnaDL">
                  <b-icon icon="archive-fill"></b-icon>
                    <span style="color: #151D65;">______</span>Product
                </div>
              </b-nav-item><br><br>
              <b-nav-item href="/transaction" @click="hide">
                <div id="warnaDL">
                  <b-icon icon="cart-fill"></b-icon>
                  <span style="color: #151D65;">______</span>Transaction
                </div>
              </b-nav-item><br><br>
              <b-nav-item href="/location" @click="hide">
                <div id="warnaDL">
                  <b-icon icon="geo-alt-fill"></b-icon>
                  <span style="color: #151D65;">_______</span>Location
                </div>
              </b-nav-item><br><br>
              
          </nav>
          
          <!-- <b-button variant="primary" block @click="hide">Close Sidebar</b-button> -->
          <br><br><br><br><br><br><br>
          <nav class="mb-1" id="logout">
            <b-nav-item href="/login" @click="logout()">
            <div id="warnaDL">
              <b-icon icon="box-arrow-in-right"></b-icon>
              Logout
            </div>
            </b-nav-item>
          </nav>
        </div>
      </template>
    </b-sidebar>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name:"Account",
  data(){
    return{
      drawer:true,
      items:[
        {name: "Account",to:"/account",icon:"person-fill"},
        {name: "Product",to:"/products"},
        {name: "Transaction",to:"/transaction"},
        {name: "Location",to:"/location"},
      ],
    };
  },
  methods: {
    logout(){
      localStorage.removeItem('token')
      this.$router.replace('/login')
    }
  }
}
</script>

<style>
  #warnaDL{
    color: white;
  }
</style>