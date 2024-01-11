<script>
import  './styles.scss'

export default {
    props: {
        produto: Object,
    },

    methods: {
        excluirProduto() {
            this.$emit('excluir-produto', this.produto);
        },

        alterarEstado() {
            this.$emit('alterar-estado', this.produto)
        }
    }
};
</script>

<template>
    <section class="card" :class="{ 'card-inativo': !produto.ativo }">
        <div class="informacoe">
            <div class="informacoe_linha">
                <p>Produto: </p>
                <p>{{ produto.nome }}</p>
            </div>
        </div>
        <div class="acoes acoes_line">
            <div class="acoes_status">
                <label>Ativo?</label>
                <button @click="alterarEstado" class="acoes_btnEstado" :class="{'acoes_btnEstado--desativado': !produto.ativo}">{{ produto.ativo? 'Sim' : 'Não' }}</button>
            </div>
            <button class="acoes_btnExcluir" @click="excluirProduto">Excluir</button>
        </div>
    </section>
</template>