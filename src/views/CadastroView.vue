<template>
  <div>
    <main>
      <div class="tela-de-cadastro">
        <h1>Inscreva-se</h1>
        <label for="name" class="nome">Nome completo</label>
        <input type="name" class="nome" placeholder="email@email.com.br" />

        <label for="email" class="email">Endereço de e-mail</label>
        <input type="email" class="email" placeholder="email@email.com.br" />

        <label for="senha" class="senha">Senha de acesso </label>
        <input type="password" class="senha" placeholder="********" />

        <router-link to="/login" class="link">Já tenho conta</router-link>
        <button class="button" @click="redirecionaPagina">Cadastrar</button>
      </div>
      <ImageLayout2Vue />
    </main>
  </div>
</template>

<script>
import ImageLayout1Vue from "@/components/ImageLayout1.vue";
import ImageLayout2Vue from "@/components/ImageLayout2.vue";

export default {
  methods: {
    redirecionaPagina() {
      this.$router.push("/entrada");
    },
  },

  components: {
    ImageLayout1Vue,
    ImageLayout2Vue,
  },
};
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;1,100;1,200;1,300&display=swap");

main {
  height: 657px;
}

.tela-de-cadastro {
  top: 68px;
  left: 31px;
}

.tela-de-cadastro > h1 {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #000e1f;
  font-weight: 800;
  font-size: 27px;
  position: absolute;
  top: 68px;
  left: 31px;
}

.tela-de-cadastro > label.nome {
  font-weight: 400;
  font-size: 16px;
  line-height: 28.8px;
  width: 157px;
  height: 29px;
  color: #000e1f;
  position: absolute;
  top: 147px;
  left: 31px;
}

.tela-de-cadastro > label.email {
  font-weight: 400;
  font-size: 16px;
  line-height: 28.8px;
  width: 157px;
  height: 29px;
  color: #000e1f;
  position: absolute;
  top: 260px;
  left: 31px;
}

.tela-de-cadastro > label.senha {
  font-weight: 400;
  font-size: 16px;
  line-height: 28.8px;
  width: 134px;
  height: 29px;
  color: #000e1f;
  position: absolute;
  top: 373px;
  left: 31px;
}

.tela-de-cadastro > input.nome {
  width: 535px;
  height: 55px;
  position: absolute;
  top: 185px;
  left: 31px;
  border: 1px solid #e5e5e5ee;
  outline: none;
  padding-left: 15px;
  font-size: 16px;
}

.tela-de-cadastro > input.email {
  width: 535px;
  height: 55px;
  position: absolute;
  top: 298px;
  left: 31px;
  border: 1px solid #e5e5e5ee;
  outline: none;
  padding-left: 15px;
  font-size: 16px;
}

.tela-de-cadastro > input.senha {
  width: 535px;
  height: 55px;
  position: absolute;
  top: 411px;
  left: 31px;
  border: 1px solid #e5e5e5ee;
  outline: none;
  padding-left: 15px;
  font-size: 16px;
}

.link {
  color: #81858e;
  text-decoration: none;
  position: absolute;
  top: 514px;
  left: 31px;
  font-size: 16px;
  width: 119px;
  height: 29px;
}

.button {
  width: 171px;
  height: 55px;
  top: 446px;
  left: 1048px;
  background-color: black;
  color: white;
  border: none;
  outline: none;
  font-family: Montserrat;
  position: absolute;
  top: 501px;
  left: 395px;
}

.button:hover {
  cursor: pointer;
}
</style>