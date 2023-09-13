<template>
  <div class="body">
    <nav class="header navbar navbar-expand-lg bg-black">
      <div class="container-fluid">
        <a class="navbar-brand ms-3" href="#">
          <img src="@/assets/emoji.png" alt="emoji" />
        </a>

        <form class="items d-flex gap-5 pe-4" role="search">
          <img
            v-b-modal.modal123
            src="@/assets/Vector.png"
            alt=""
            class="Vector"
          />

          <b-modal
            centered
            id="modal123"
            ok-variant="dark"
            foot
            hide-header
            modal-ok
            size="lg"
          >
            <div class="modalVue p-3">
              <input
                class="modalInputTitle mb-2 d-block"
                type="text"
                placeholder="Nome da tarefa"
                v-model="novoTitulo"
              />

              <input
                class="modalInputDesc mb-3"
                type="text"
                placeholder="Descrição"
                v-model="novaDescricao"
              />

              <input
                type="datetime-local"
                id="datetimePicker"
                name="datetimePicker"
                v-model="novaData"
              />
            </div>
            <template v-slot:modal-footer="{ hide }">
              <b-button
                class="cancelaTarefa"
                variant="secondary"
                @click="hide()"
              >
                Cancelar
              </b-button>
              <b-button class="criaTarefa" variant="dark" @click="enviarTarefa">
                Criar tarefa
              </b-button>
            </template>
          </b-modal>

          <img src="@/assets/Interrogacao.png" alt="" class="Interrogacao" />
          <img src="@/assets/Sino.png" alt="" class="Sino" />
          <img src="@/assets/L.png" alt="" class="L" />
        </form>
      </div>
    </nav>

    <aside>
      <ul>
        <div>
          <img src="@/assets/Entrada.png" alt="" />
          <li class="d-inline">Entrada</li>
        </div>
        <div>
          <img src="@/assets/Tarefas.png" alt="" />
          <li class="d-inline">Tarefas de hoje</li>
        </div>
        <div>
          <img src="@/assets/Vencido.png" alt="" />
          <li>Vencidos</li>
        </div>
      </ul>
    </aside>

    <main>
      <h1>Entrada</h1>
      <div class="cards">
        <div class="carde" v-for="(tarefa, index) in tarefas" :key="index">
          <div class="carde-content mt-2">
            <b-form-checkbox
              class="ms-2"
              :id="'check' + tarefa.id"
              :name="'checkbox' + tarefa.id"
              :checked="estaMarcado(tarefa)"
              @change="completaTarefa(tarefa)"
            >
            </b-form-checkbox>

            <label class="title" v-b-modal="'modal' + tarefa.id">{{
              tarefa.titulo
            }}</label>
            <p class="description mb-3">{{ tarefa.descricao }}</p>
            <p class="date" :style="{ color: trocaCor(tarefa, false), backgroundColor: trocaCor(tarefa, true)}">
              {{ formatCreatedAtwDMS(tarefa.data_vencimento) }}
            </p>
            <div class="crud-icons">
              <img
                v-b-modal="'modal' + tarefa.id"
                src="@/assets/EditarTarefa.png"
                alt="Editar Tarefa"
                class="EditarTarefa"
              />
              <img
                src="@/assets/DefinirVencimento.png"
                alt="Definir Vencimento"
                class="DefinirVencimento"
              />
              <img
                src="@/assets/ExcluirTarefa.png"
                alt="Excluir Tarefa"
                class="ExcluirTarefa"
                @click="apagaTarefa(tarefa.id)"
              />
            </div>
          </div>

          <div class="carde subcarde" v-for="(subtarefa, index) in tarefa.subtarefas" :key="index">
            <div class="carde-content">
              <b-form-checkbox
                class="ms-2"
                :id="'check' + subtarefa.id"
                :name="'checkbox' + subtarefa.id"
                :checked="estaMarcado(subtarefa)"
                @change="completaTarefa(subtarefa)"
              >
              </b-form-checkbox>

              <label class="title" v-b-modal="'modal' + subtarefa.id">{{ subtarefa.titulo }}</label>
              <p class="description mb-3">{{ subtarefa.descricao }}</p>

              <div class="crud-icons">
                <img
                  v-b-modal="'modal' + tarefa.id"
                  src="@/assets/EditarTarefa.png"
                  alt="Editar Tarefa"
                  class="EditarTarefa"
                />
                <img
                  src="@/assets/DefinirVencimento.png"
                  alt="Definir Vencimento"
                  class="DefinirVencimento"
                />
                <img
                  src="@/assets/ExcluirTarefa.png"
                  alt="Excluir Tarefa"
                  class="ExcluirTarefa"
                  @click="apagaTarefa(tarefa.id)"
                />
              </div>
            </div>
          </div>

          <b-modal
            hide-footer
            size="xl"
            class="visualizar-tarefa"
            :id="'modal' + tarefa.id"
          >
            <div class="modal-conteudo">
              <div class="subtarefas-modal">
                <label class="title-modal">{{ tarefa.titulo }}</label>
                <p class="description-modal">{{ tarefa.descricao }}</p>
                <label class="subtitle-modal">Subtarefas</label>
                <hr />
                <div v-for="(subtarefa, index) in tarefa.subtarefas" :key="index">
                  <p>{{ subtarefa.titulo }}</p>
                </div>
              </div>
              <aside class="modalAside">
                <div class="content-aside">
                  <div class="criadoEm">Criado em</div>
                  <div class="criadoEmData">{{ formatCreatedAt(tarefa.created_at) }}</div>
                  <div class="criadoEm">Data de vencimento</div>
                  <div
                    class="criadoEmData"
                    :style="{
                      color: trocaCor(tarefa, false),
                      background: trocaCor(tarefa, true),
                    }"
                  >
                    {{ formatCreatedAtwDMS(tarefa.data_vencimento) }}
                  </div>
                  <div class="criadoEm">Modificado em</div>
                  <div class="criadoEmData">{{ formatCreatedAt(tarefa.updated_at) }}</div>
                  <div>ID da tarefa</div>
                  <div>{{ tarefa.id }}</div>
                </div>
              </aside>
            </div>
          </b-modal>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import moment from "moment";
import emoji from "@/assets/emoji.png";
import Entrada from "@/assets/Entrada.png";
import axios from "axios";

export default {
  data() {
    return {
      tarefas: [],
      novoTitulo: "",
      novaData: "",
      novaDescricao: "",
      novoStatus: "",
    };
  },

  methods: {
    buscaTarefas() {
      fetch("http://localhost:8000/tasks/")
        .then((data) => {
          return data.json();
        })
        .then((data) => {
          this.tarefas = data;
        });
    },

    estaMarcado(tarefa) {
      if (tarefa.status === "completa") {
        return true;
      } else {
        return "pendente";
      }
    },

    trocaCor(tarefa, is_bk) {
      if (!tarefa) {
        return;
      }
      const dataAtual = new Date();
      const dataVencimento = new Date(tarefa.data_vencimento);
      if (is_bk) {
        if (dataVencimento < dataAtual) {
          return "#D314081A"; 
        } else {
          return "#0094881A";
        }
      }
      if (dataVencimento < dataAtual) {
        return "#D31408"; // Define a cor como verde para datas vencidas
      } else {
        return "#009488"; // Define a cor como vermelha para datas futuras ou iguais
      }
    },

    formatCreatedAt(created_at) {
      return moment(created_at).format("DD/MM/YYYY HH:mm:ss");
    },

    formatCreatedAtwDMS(created_at) {
      return moment(created_at).format("DD/MM/YYYY");
    },

    enviarTarefa() {
      const criaTarefa = {
        titulo: this.novoTitulo,
        descricao: this.novaDescricao,
        data_vencimento: this.novaData,
        status: "pendente",
      };

      fetch("http://localhost:8000/tasks/", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(criaTarefa),
      })
        .then((response) => response.json())
        .then((data) => {
          this.tarefas.push(data);
          this.$bvModal.hide("modal123");
          this.buscaTarefas();
        })
        .catch((error) => {
          console.log("Erro ao criar a tarefa:", error);
        });
    },

    apagaTarefa(id) {
      fetch(`http://localhost:8000/tasks/${id}`, {
        method: "DELETE",
      })
        .then((response) => {
          if (response.ok) {
            this.tarefas = this.tarefas.filter((tarefa) => tarefa.id !== id);
          } else {
            console.log("Erro ao excluir a tarefa:", response.statusText);
          }
        })
        .catch((error) => {
          console.error("Erro ao excluir a tarefa:", error);
        });
    },

    completaTarefa(tarefa) {
      const novoStatus = tarefa.status === "pendente" ? "completa" : "pendente";

      const atualizacao = {
        titulo: tarefa.titulo,
        descricao: tarefa.descricao,
        data_vencimento: tarefa.data_vencimento,
        status: novoStatus,
      };

      fetch(`http://localhost:8000/tasks/${tarefa.id}`, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(atualizacao),
      })
        .then((response) => {
          if (response.status === 200) {
            // Atualize o status localmente após a confirmação do servidor
            this.tarefas = this.tarefas.map((t) => {
              if (t.id === tarefa.id) {
                return { ...t, status: novoStatus };
              } else {
                return t;
              }
            });
          } else {
            console.log("Erro ao atualizar a tarefa:", response.statusText);
          }
        })
        .catch((error) => {
          console.error("Erro ao atualizar a tarefa:", error);
        });
    },
  },

  created() {
    this.buscaTarefas(), this.trocaCor();
  },
};
</script>

<style lang="scss" scoped>
.body {
  font-family: Montserrat, sans-serif;
}

.header {
  height: 70px;
}

.items {
  align-items: center;
}

.Vector {
  height: 14px;
  width: 14px;
}

.Interrogacao {
  height: 20px;
  width: 20px;
}

.Sino {
  height: 20px;
  width: 18px;
}

.L {
  width: 30px;
  height: 30px;
}

.emoji {
  height: 28px;
  width: 28px;
}

aside {
  width: 293px;
  background-color: #fafafa;
  height: 100vh;
}

ul {
  list-style-type: none;
  width: 231px;
  height: 159.1px;
  position: absolute;
  top: 120px;
  left: 31px;
}

li {
  font-size: 16px;
  color: black;
  font-weight: 600;
  line-height: 18.29px;
  display: inline;
  margin-left: 16px;
}

ul > div {
  margin-bottom: 35px;
  margin-top: 20px;
}

main > .cards {
  position: absolute;
  left: 458px;
  top: 179px;
  width: 678px;
  height: 100%;
}

main > h1 {
  position: absolute;
  left: 458px;
  top: 120px;
  font-weight: 800;
  font-size: 24px;
  line-height: 29.26px;
  color: black;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

.carde {
  height: 109px !important;
  border: 1px solid #e5e5e5;
  margin-bottom: 25px;
}

.carde-content {
  height: 79px;
  width: 462px;
}

.carde-content > .title {
  font-weight: 400;
  font-size: 16px;
  line-height: 19.5px;
  color: black;
  display: inline !important;
  margin-left: 28px;
}

.carde-content > .custom-control {
  accent-color: black !important;
  display: inline !important;
}

.carde-content > .date {
  margin-left: 50px;
  font-size: 14px;
  font-weight: 600;
  line-height: 17.07px;
  color: #000000;
  font-family: Montserrat, sans-serif;
  width: 80px;
  padding: 4px;
}

.carde-content > .description {
  margin-left: 47px;
  margin-top: 5px;
  display: block;
  font-size: 14px;
  color: #81858e;
  font-weight: 400;
  line-height: 17.07px;
  width: 477px;
  white-space: nowrap; /* Impede que o texto quebre em várias linhas */
  overflow: hidden; /* Esconde o texto que não cabe no contêiner */
  text-overflow: ellipsis;
}

.crud-icons {
  margin-left: 525px;
  display: flex;
  margin-top: -65px;
}

.EditarTarefa,
.DefinirVencimento,
.ExcluirTarefa {
  margin-left: 25px;
  cursor: pointer;
}

.modalInputTitle,
.modalInputDesc {
  border: none !important;
  outline: none !important;
}

.modalInputTitle {
  font-size: 18px;
  font-weight: 600;
  color: black;
  width: 276px;
  margin-bottom: 4px;
}

.modalInputDesc {
  font-size: 16px;
  font-weight: 400;
  color: #81858e;
  width: 447px;
}

.criaTarefa {
  background-color: black !important;
  height: 40px !important;
  width: 122px !important;
  border-radius: 0 !important;
}

.cancelaTarefa {
  background-color: #f7f7f7 !important;
  height: 40px !important;
  width: 102px !important;
  border-radius: 0 !important;
  border: none !important;
  color: black !important;
}

#datetimePicker {
  display: block !important;
  margin-right: 12px !important;
}

.title-modal {
  color: black !important;
  font-weight: 600 !important;
  font-size: 18px !important;
  line-height: 21.94px !important;
}

.description-modal {
  color: #81858e !important;
  font-weight: 400 !important;
  font-size: 14px !important;
  line-height: 21px !important;
  width: 470px !important;
  height: 42px !important;
}

.modal-conteudo {
  display: grid;
  grid-template-columns: 1fr 247px;
  justify-content: space-between;
}

.modalAside {
  background-color: #f7f7f7 !important;
  width: 246px !important;
  height: 548px !important;
  display: flex !important;
  flex-direction: column !important;
}

.modal-custom-checkbox {
  height: 20px;
  width: 20px;
  accent-color: black;
}

.subtitle-modal {
  color: #000000;
  font-size: 15px;
  line-height: 17.07px;
  font-weight: 600;
  font-family: Montserrat;
}

.subtarefas-modal {
  margin-left: 60px;
  margin-top: 30px;
  width: 470px;
  height: 113px;
}

.content-aside {
  padding: 30px;
  position: relative;
}

.criadoEm {
  color: #81858e;
  font-size: 14px;
  line-height: 17.07px;
  margin-bottom: 5px;
}

.criadoEmData {
  font-size: 14px;
  font-weight: 600;
  line-height: 17.07px;
  color: #000000;
  font-family: Montserrat, sans-serif;
  margin-bottom: 40px;

  
}
</style>




