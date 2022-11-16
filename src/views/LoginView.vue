<template>
  <div class="login login-background">
    <v-container class="login">
      <v-row class="login" justify="center" align="center">
        <v-card outlined width="25%" class="login-card">
          <v-card-title>
            <img src="../assets/fc-logo.svg">
          </v-card-title>
          <v-card-text>
            <v-text-field dark color="green" type="email" dense placeholder="exemplo@hotmail.com" outlined v-model="login" label="Login"
              required>
            </v-text-field>
            <v-text-field dark color="green" type="password" dense outlined v-model="password" label="Senha" required>
            </v-text-field>
            <v-btn variant="flat" @click="goToTable" color="#CF1030" width="100%"><span class="btn-title">Entrar</span>
            </v-btn>
          </v-card-text>
        </v-card>
      </v-row>
    </v-container>
  </div>
</template>

<script>

export default {
  name: 'LoginView',

  data: () => ({
    login: "",
    password: "",
  }),

  methods: {
    goToTable() {
      this.$router.push("/table")
    }
  }
}
</script>

<style scoped>
.login {
  height: 100%;
}

.login-background {
  background-image: url("https://mir-s3-cdn-cf.behance.net/project_modules/fs/108e1b140262313.623e112561f0d.png");
  background-repeat: no-repeat;
  background-size: cover;
}

.login-card {
  background: rgba(0, 0, 0, 0.5);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(9.5px);
  -webkit-backdrop-filter: blur(9.5px);
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.18);
}

.btn-title {
  color: white;
}
</style>
