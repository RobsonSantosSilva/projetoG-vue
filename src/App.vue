<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}


.modal-body, 
 .modal-content { 
   border-radius: 0px !important; 
   padding: 0px !important;
 }

 .close {
    border: 0px;
    background-color: transparent;
    font-size: 20px;
 }

 .subcarde {
    height: fit-content !important;
    padding-left: 12px !important;
  }

  .custom-control-input{
    margin: 8px 0;
  }

</style>
