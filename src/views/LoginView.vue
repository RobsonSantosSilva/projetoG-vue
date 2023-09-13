<template>
  <div>
    <main>
        <ImageLayout1/>

        <div class="tela-de-login">
            <h1>Login</h1>
            <label for="email" class="email">Endereço de e-mail</label>
            <input type="email" class="email" placeholder="email@mail.com.br">

            <label for="password" class="senha">Senha de acesso </label>
            <input type="password" class="senha" placeholder="********">
            
             
            <router-link to="/cadastro" class="link">Não tenho conta</router-link>

             
            <button class="button" @click="redirecionaPagina">Acessar</button>
        </div>
    </main>
  </div>
</template>

<script>

import ImageLayout1 from '@/components/ImageLayout1.vue';

export default {
    components: {
        ImageLayout1
    },

    methods: {
        redirecionaPagina(){
            this.$router.push('/entrada');
        }
    }
}
</script>

<style lang="scss" scoped>

@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;1,100;1,200;1,300&display=swap');

main {
    display: grid !important;
    grid-template-columns: 1fr 1fr !important;
    height: 657px !important;
    margin: auto;
    font-family: Montserrat, sans-serif;
}

.tela-de-login{
    width: 535px;
    height: 375px;
    top: 126px;
    left: 684px;
}

.tela-de-login > h1 {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    color: #000E1F;
    font-weight: 800;
    font-size: 27px;
    position: absolute;
    top: 126px;
    left: 684px;
}

.tela-de-login > label.email {
    font-weight: 400;
    font-size: 16px;
    line-height: 28.8px;
    width: 157px;
    height: 29px;
    color: #000E1F;
    position: absolute;
    top: 205px;
    left: 684px;
}

.tela-de-login > label.senha {
    font-weight: 400;
    font-size: 16px;
    line-height: 28.8px;
    width: 134px;
    height: 29px;
    top: 318px;
    left: 684px;
    color: #000E1F;
    position: absolute;
}

.tela-de-login > input.email {
    width: 535px;
    height: 55px;
    position: absolute;
    top: 243px;
    left: 684px;
    border: 1px solid #E5E5E5EE;
    outline: none;
    padding-left: 15px;
}

.tela-de-login > input.senha {
    width: 535px;
    height: 55px;
    position: absolute;
    top: 356px;
    left: 684px;
    border: 1px solid #E5E5E5EE;
    outline: none;
    padding-left: 15px;
}

.tela-de-login > a {
    position: absolute;
    top: 459px;
    left: 684px;
}

.link {
    color: #81858E;
    text-decoration: none;
    width: 135px;
    height: 29px;
}

.button {
  width: 171px;
  height: 55px;
  background-color: black;
  color: white;
  border: none;
  outline: none;
  font-family: Montserrat;
  position: relative;
  top: 446px;
  left: 1048px;
}

</style>

