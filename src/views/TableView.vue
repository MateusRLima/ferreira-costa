<template >
  <div class="table table-background">
    <v-container class="table">
      <v-row>
        <v-toolbar elevation="4" class="mb-5 rounded" dense>
          <v-btn @click="returnToLogin" icon small v-bind="attrs" v-on="on">
            <v-icon>
              mdi-logout
            </v-icon>
          </v-btn>
          <v-spacer></v-spacer>
          <span>Bem vindo !</span>
          <v-spacer></v-spacer>
        </v-toolbar>
      </v-row>
      <v-row>
        <v-card class="rounded">
          <v-card-text>
            <v-data-table :headers="header" :items="users" item-key="cpf" :search="search">
              <template v-slot:top>
                <v-container>
                  <v-row>
                    <v-text-field v-model="search" outlined dense label="Search" prepend-inner-icon="mdi-magnify" class="mx-4" />
                    <v-spacer></v-spacer>
                    <dialog-form class="" />
                  </v-row>
                </v-container>
              </template>
              <template v-slot:[`item.status`]="{ item }">
                <span v-if="item.status === 1">Ativo</span>
                <span v-else-if="item.status === 2">Inativo</span>
                <span v-else-if="item.status === 3">Bloqueado</span>
              </template>
              <template v-slot:[`item.acoes`]="{ item }">
                <v-tooltip color="#0C0C0C" bottom>
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn @click="blockUser(item.cpf)" small icon color="red" v-bind="attrs" v-on="on">
                      <v-icon small>mdi-cancel</v-icon>
                    </v-btn>
                  </template>
                  <p class="text-caption secondary-font ma-0">Bloquear</p>
                </v-tooltip>
              </template>
            </v-data-table>
          </v-card-text>
        </v-card>
      </v-row>
    </v-container>
  </div>
</template>
<script>

import users from "@/utils/UserData"
import DialogFormVue from "@/components/DialogForm.vue";

export default {
  data: () => ({
    users: users,
    search: "",
  }),

  components: {
    "dialog-form": DialogFormVue
  },

  computed: {
    header() {
      return [
        { text: "Nome", value: "nome" },
        { text: "Login", value: "login" },
        { text: "E-mail", value: "email" },
        { text: "Senha", value: "senha", sortable: false, hide: true },
        { text: "Telefone", value: "telefone", sortable: false },
        { text: "CPF", value: "cpf", sortable: false },
        { text: "Data de Nascimento", value: "dataNascimento" },
        { text: "N° Mãe", value: "nomeMae" },
        { text: "Status", value: "status" },
        { text: "Data Criação", value: "dataInclusao" },
        { text: "Data Alteração", value: "dataAlteracao", divider: true },
        { text: "Ações", value: "acoes" },
      ]
    }
  },

  methods: {
    blockUser(cpf) {
      for (let index = 0; index < users.length; index++) {
        const element = users[index];
        if (cpf === element.cpf) {
          element.status = 3
        }
      }
    },

    returnToLogin() {
      this.$router.push("/")
    }
  }
}
</script>
<style scoped>
.table-background {
  background-image: url("https://mir-s3-cdn-cf.behance.net/project_modules/fs/108e1b140262313.623e112561f0d.png");
  background-repeat: no-repeat;
  background-size: cover;
}

.table {
  height: 100%;
}

.rounded {
  border-radius: 10px;
}
</style>
