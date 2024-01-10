<script>
import './styles.scss'
import ItemLista from '../components/ItemListaCliente/index.vue'
import FormCliente from '../components/FormCadastro/Cliente.vue'

export default {
    emits: ['cadastrar'],

    data() {
        return {
        mostrarFormulario: false,
        clientes: [],
        mensagemBTN: 'Cadastrar'
        };
    },
    methods: {
        btnPrincipal(){
            if(this.mostrarFormulario === false){
                this.mostrarFormulario = true
                this.mensagemBTN = 'Cancelar'
            } else {
                this.mostrarFormulario = false
                this.mensagemBTN = 'Cadastrar'
            }
        },
        cadastrarCliente(cliente) {
            this.clientes.push(cliente);
            this.mostrarFormulario = false;
            this.mensagemBTN = 'Cadastrar'
        },
    },
    components: {
        FormCliente,
        ItemLista
    },
};
</script>

<template>
    <button @click="btnPrincipal" class="btn-cadastrar" :class="{'btn-cadastrar--cancelar': mensagemBTN === 'Cancelar'}">{{ mensagemBTN }}</button>
    <FormCliente v-if="mostrarFormulario" @cadastrar="cadastrarCliente" />
    <ul class="list">
        <li class="list_item">
            <ItemLista v-for="(cliente, index) in clientes" :key="index" :cliente="cliente" />
        </li>
    </ul>
</template>