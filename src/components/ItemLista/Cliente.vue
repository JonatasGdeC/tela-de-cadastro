<script>
import './styles.scss'

export default {
  props: {
    cliente: Object,
  },

  methods: {
    excluirCliente() {
      this.$emit('excluir-cliente', this.cliente)
    },

    alterarEstado() {
      this.$emit('alterar-estado', this.cliente)
    },
  },
}
</script>

<template>
  <section class="card" :class="{ 'card-inativo': !cliente.ativo }">
    <div class="informacoe">
      <div class="informacoe_linha">
        <p>Nome:</p>
        <p>{{ cliente.nome }}</p>
      </div>
      <div class="informacoe_linha">
        <p>CPF:</p>
        <p>{{ cliente.cpf }}</p>
      </div>
      <div class="informacoe_linha">
        <p>Telefone:</p>
        <p>{{ cliente.telefone }}</p>
      </div>
      <div class="informacoe_linha">
        <p>Email:</p>
        <p>{{ cliente.email }}</p>
      </div>
    </div>
    <div class="acoes">
      <div class="acoes_status">
        <label>Ativo?</label>
        <button
          @click="alterarEstado"
          class="acoes_btn acoes_btn_status"
          :class="{ 'acoes_btn_status--desativado': !cliente.ativo }"
          title="Alterar status"
        >
          {{ cliente.ativo ? 'Sim' : 'Não' }}
        </button>
      </div>
      <button class="acoes_btn acoes_btn_excluir" @click="excluirCliente">
        Excluir
      </button>
    </div>
  </section>
</template>
