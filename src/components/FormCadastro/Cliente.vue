<script>
import VueMask from 'vue-the-mask'
import './styles.scss'

export default {
  data() {
    return {
      nome: '',
      cpf: '',
      telefone: '',
      email: '',
    }
  },
  directives: {
    mask: VueMask.directive,
  },
  methods: {
    cadastrar() {
      const dadosCliente = {
        nome: this.nome,
        cpf: this.cpf,
        telefone: this.telefone,
        email: this.email,
        produtos: [],
      }

      const verificando = () => {
        this.nome.length < 3
          ? alert('O nome do cliente deve conter de 3 a 20 caracteres...')
          : this.cpf.length < 11
            ? alert('CPF do cliente deve conter 11 números...')
            : this.telefone.length < 11
              ? alert('Digite um número de celular com DDD...')
              : this.$emit('cadastrar', dadosCliente)
      }
      verificando()
    },
  },
}
</script>

<template>
  <div class="form">
    <form>
      <div class="form_campo">
        <label class="form_campo_nome" for="name">Nome:</label>
        <input
          class="form_campo_input"
          v-model="nome"
          id="name"
          type="text"
          minlength="3"
          maxlength="50"
        />
      </div>
      <div class="form_campo">
        <label class="form_campo_nome" for="cpf">CPF:</label>
        <input
          class="form_campo_input"
          v-model="cpf"
          id="cpf"
          type="number"
          placeholder="XXX.XXX.XXX-XX"
          v-mask="'###.###.###-##'"
        />
      </div>
      <div class="form_campo">
        <label class="form_campo_nome" for="contato">Contato:</label>
        <input
          class="form_campo_input"
          v-model="telefone"
          id="contato"
          type="tel"
          placeholder="(XX) XXXXX-XXXX"
          maxlength="11"
          v-mask="'(##) ####-####'"
        />
      </div>
      <div class="form_campo">
        <label class="form_campo_nome" for="email">Email:</label>
        <input
          class="form_campo_input"
          v-model="email"
          id="email"
          type="email"
        />
      </div>
    </form>
    <button class="form_button" @click="cadastrar">Cadastrar</button>
  </div>
</template>
