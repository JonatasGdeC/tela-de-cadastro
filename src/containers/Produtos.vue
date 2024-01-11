<script>
import './styles.scss'
import FormProduto from '../components/FormCadastro/Produto.vue'
import ItemListaProdutos from '../components/ItemLista/Produto.vue'

export default {
    emits: ['cadastrar'],

    data(){
        return{
            mostrarFormulario: false,
            mensagemBTN: 'Cadastrar',
            produtos: [],
            produtosInativos: [],
        }
    },

    mounted(){
        this.carregarDadosDoLocalStorage();
    },

    beforeUnmount(){
        this.salvarDadosNoLocalStorage();
    },

    methods: {
        carregarDadosDoLocalStorage() {
            const storedProdutos = localStorage.getItem('produtos');
            const storedProdutosInativos = localStorage.getItem('produtosInativos');
            
            if (storedProdutos) {
                this.produtos = JSON.parse(storedProdutos);
            }

            if (storedProdutosInativos) {
                this.produtosInativos = JSON.parse(storedProdutosInativos);
            }
        },

        salvarDadosNoLocalStorage() {
            const jsonStringProdutos = JSON.stringify(this.produtos);
            const jsonStringProdutosInativos = JSON.stringify(this.produtosInativos);

            localStorage.setItem('produtos', jsonStringProdutos);
            localStorage.setItem('produtosInativos', jsonStringProdutosInativos);
        },

        btnPrincipal(){
            if(this.mostrarFormulario === false){
                this.mostrarFormulario = true
                this.mensagemBTN = 'Cancelar'
            } else{
                this.mostrarFormulario = false
                this.mensagemBTN = 'Cadastrar'
            }
        },

        cadastrarProduto(produto) {
            this.produtos.push(produto);
            this.mostrarFormulario = false;
            this.mensagemBTN = 'Cadastrar'

            // Atualiza o localStorage após cadastrar um novo produto
            const jsonString = JSON.stringify(this.produtos);
            localStorage.setItem('produtos', jsonString);
        },

        alterarEstadoProduto(produto){
            produto.ativo = !produto.ativo;
            // Move o produto para a lista de produtos inativos, se estiver inativo
            if (!produto.ativo) {
                const index = this.produtos.indexOf(produto);
                if (index !== -1) {
                    this.produtos.splice(index, 1);
                    this.produtosInativos.push(produto);
                }
            } else {
                // Move o produto de volta para a lista de produtos ativos, se estiver ativo novamente
                const index = this.produtosInativos.indexOf(produto);
                if (index !== -1) {
                    this.produtosInativos.splice(index, 1);
                    this.produtos.push(produto);
                }
            }
            // Atualiza o localStorage após alterar o estado do produto
            const jsonString = JSON.stringify(this.produtos);
            localStorage.setItem('produtos', jsonString);
        },

        excluirProdutoDoLocalStorage(produto){
            // Encontrar e excluir o produto da matriz no estado
            const index = this.produtos.indexOf(produto);
            if (index !== -1) {
                this.produtos.splice(index, 1);

                // Atualizar o localStorage após excluir o produto
                const jsonString = JSON.stringify(this.produtos);
                localStorage.setItem('produtos', jsonString);
            }
        }
    },
    components: {
        FormProduto,
        ItemListaProdutos
    }
}
</script>

<template>
    <button @click="btnPrincipal" class="btn-cadastrar" :class="{'btn-cadastrar--cancelar': mensagemBTN === 'Cancelar'}">{{ mensagemBTN }}</button>
    <FormProduto v-if="mostrarFormulario" @cadastrar="cadastrarProduto" />
    <ul class="list">
        <li class="list_item">
            <ItemListaProdutos v-for="(produto, index) in produtos" :key="index" :produto="produto" @excluir-produto="excluirProdutoDoLocalStorage" @alterar-estado="alterarEstadoProduto"/>
        </li>
    </ul>

    <!-- Lista de produtos Inativos -->
    <ul class="list--inativos">
        <li class="list_item">
            <ItemListaProdutos v-for="(produto, index) in produtosInativos" :key="index" :produto="produto" @excluir-produto="excluirProdutoDoLocalStorage" @alterar-estado="alterarEstadoProduto" />
        </li>
    </ul>
</template>