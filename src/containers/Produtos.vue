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
            produtos: []
        }
    },
    methods: {
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
        },
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
            <ItemListaProdutos v-for="(produto, index) in produtos" :key="index" :produto="produto" />
        </li>
    </ul>
</template>