<script>
import './styles.scss'

export default {
    props: {
        cliente: Object,
    },

    methods: {
        excluirCliente() {
            this.$emit('excluir-cliente', this.cliente);
        },

        alterarEstado() {
            this.$emit('alterar-estado', this.cliente)
        }
    }
};

</script>

<template>
    <section class="card" :class="{ 'card-inativo': !cliente.ativo }">
        <div class="informacoe">
            <div class="informacoe_linha">
                <p>Nome:</p>
                <p>{{ cliente.nome }}</p>
            </div>
            <div class="informacoe_linha">
                <p>CPF: </p>
                <p>{{ cliente.cpf }}</p>
            </div>
            <div class="informacoe_linha">
                <p>Telefone: </p>
                <p>{{ cliente.telefone }}</p>
            </div>
            <div class="informacoe_linha">
                <p>Email: </p>
                <p>{{ cliente.email }}</p>
            </div>
        </div>
    <div class="acoes">
        <div class="acoes_status">
            <label>Ativo?</label>
            <button @click="alterarEstado" class="acoes_btnEstado" :class="{'acoes_btnEstado--desativado': !cliente.ativo}">{{ cliente.ativo? 'Sim' : 'Não' }}</button>
        </div>
        <button class="acoes_btnExcluir" @click="excluirCliente">Excluir</button>
    </div>
    </section>
</template>