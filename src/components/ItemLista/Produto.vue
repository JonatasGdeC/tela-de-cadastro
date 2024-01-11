<script>
import  './styles.scss'

export default {
    props: {
        produto: Object,
    },

    methods: {
        excluirProduto() {
            this.$emit('excluir-produto', this.produto);
        }
    }
};
</script>

<template>
    <section class="card">
        <div class="informacoe">
            <div class="informacoe_linha">
                <p>Produto: </p>
                <p>{{ produto.nome }}</p>
            </div>
        </div>
        <div class="acoes">
            <form>
                <label>Ativo?</label>
                <select>
                    <option>Sim</option>
                    <option>Não</option>
                </select>
            </form>
            <button class="acoes_btnExcluir" @click="excluirProduto">Excluir</button>
        </div>
    </section>
</template>