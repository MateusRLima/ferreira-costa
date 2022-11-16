<template >
	<div>
		<v-dialog v-model="dialog" width="500">
			<template v-slot:activator="{ on, attrs }">
				<v-tooltip  color="#0C0C0C" bottom v-bind="attrs" v-on="on">
					<template v-slot:activator="{ on, attrs }">
						<v-btn dark fab small v-bind="attrs" v-on="on">
							<v-icon>
								mdi-plus
							</v-icon>
						</v-btn>
					</template>
					<p class="text-caption secondary-font ma-0">Incluir</p>
				</v-tooltip>
			</template>

			<v-card>
				<v-card-title>
					Incluir Usuário
				</v-card-title>

				<v-card-text>
					<v-text-field type="text" dense outlined v-model="user.nome" label="Nome" required>
					</v-text-field>
					<v-text-field type="text" dense outlined v-model="user.login" label="Login" required>
					</v-text-field>
					<v-text-field type="email" dense placeholder="exemplo@hotmail.com" outlined v-model="user.email"
						label="E-mail" required>
					</v-text-field>
					<v-text-field type="password" dense outlined v-model="user.password" label="Senha" required>
					</v-text-field>
					<v-text-field dense outlined v-model="user.telefone" v-mask="'(##) # ####-####'" label="Telefone"
						required>
					</v-text-field>
					<v-text-field dense outlined v-model="user.cpf" v-mask="'###.###.###-##'" label="CPF" required>
					</v-text-field>
					<v-text-field dense outlined v-model="user.dataNascimento" v-mask="'##/##/####'"
						label="Data de Nascimento" required>
					</v-text-field>
					<v-text-field type="text" dense outlined v-model="user.nomeMae" label="Nome da Mãe" required>
					</v-text-field>
				</v-card-text>

				<v-divider></v-divider>

				<v-card-actions>
					<v-btn outlined @click="dialog = false">
						Cancelar
					</v-btn>
					<v-spacer></v-spacer>
					<v-btn outlined @click="createUser()">
						Criar
					</v-btn>
				</v-card-actions>
			</v-card>
		</v-dialog>
	</div>
</template>
<script>
import users from '@/utils/UserData';

export default {
	name: "DialogFormVue",

	data: () => ({
		dialog: false,
		user: {
			nome: "",
			login: "",
			email: "",
			senha: "",
			telefone: "",
			cpf: "",
			dataNascimento: "",
			nomeMae: "",
			status: "",
			dataInclusao: "",
			dataAlteracao: "",
		}
	}),

	methods: {

		padTo2Digits(num) {
			return num.toString().padStart(2, '0');
		},

		formatDate(date) {
			return [
				this.padTo2Digits(date.getDate()),
				this.padTo2Digits(date.getMonth() + 1),
				date.getFullYear(),
			].join('/');
		},

		createUser() {
			this.user.dataInclusao = this.formatDate(new Date())
			this.user.dataAlteracao = this.formatDate(new Date())

			users.push(this.user)
		}
	}
}
</script>
<style>

</style>