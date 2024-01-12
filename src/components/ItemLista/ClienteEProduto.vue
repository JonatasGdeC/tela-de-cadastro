<script>

export default {
    props: {
        cliente: Object,
        produtos: Array
    },

    data() {
        return {
            produtoSelecionado: ''
        }
    },

    mounted() {
        this.cliente.produtos = this.cliente.produtos || [];
        const produtosAssociados = JSON.parse(localStorage.getItem(`produtos_cliente_${this.cliente.id}`));
        this.cliente.produtos = produtosAssociados || [];
},

    methods: {
        adicionarProduto() {
            this.cliente.produtos = this.cliente.produtos || [];

            if (this.produtoSelecionado) {
                // Adiciona o produto selecionado à lista de produtos associados ao cliente
                this.cliente.produtos.push({ nome: this.produtoSelecionado });
                
                // Atualiza o localStorage após adicionar o produto
                this.atualizarLocalStorage();
            }
            console.log('Produto selecionado:', this.produtoSelecionado);
        },

        atualizarLocalStorage() {
            console.log('Produtos associados:', this.cliente.produtos);
            localStorage.setItem(`produtos_cliente_${this.cliente.id}`, JSON.stringify(this.cliente.produtos));
        },
    }
}

</script>

<template>
    <section class="card">
        <div class="informacoe">
            <div class="informacoe_linha">
                <p>Cliente: </p>
                <p>{{ cliente.nome }}</p>
            </div>
            <div class="informacoe_linha">
                <p>Produtos: </p>
                <select v-model="produtoSelecionado">
                    <option v-for="produto in produtos" :key="produto.id">{{ produto.nome }}</option>
                </select>
            </div>
            <ul>
                <li v-for="produto in cliente.produtos" :key="produto.nome">{{ produto.nome }}</li>
            </ul>
        </div>
        <div class="acoes">
            <button @click="adicionarProduto">Adicionar Produto</button>
        </div>
    </section>
</template>