<script>
import './styles.scss'
import FormCliente from '../components/FormCadastro/Cliente.vue'
import ItemListaClientes from '../components/ItemLista/Cliente.vue'

export default {
    emits: ['cadastrar'],

    data() {
        return {
        mostrarFormulario: false,
        mensagemBTN: 'Cadastrar',
        clientes: []
        };
    },

    mounted() {
        // Recupera os dados do localStorage quando o componente é montado
        const storedClientes = localStorage.getItem('clientes');
        if (storedClientes) {
            this.clientes = JSON.parse(storedClientes);
        }
    },

    beforeUnmount() {
        // Salva os dados no localStorage antes de desmontar o componente
        const jsonString = JSON.stringify(this.clientes);
        localStorage.setItem('clientes', jsonString);
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

            // Atualiza o localStorage após cadastrar um novo cliente
            const jsonString = JSON.stringify(this.clientes);
            localStorage.setItem('clientes', jsonString);
        },
        excluirClienteDoLocalStorage(cliente){
            // Encontrar e excluir o cliente da matriz no estado
            const index = this.clientes.indexOf(cliente);
            if (index !== -1) {
                this.clientes.splice(index, 1);

                // Atualizar o localStorage após excluir o cliente
                const jsonString = JSON.stringify(this.clientes);
                localStorage.setItem('clientes', jsonString);
            }
        }
    },
    components: {
        FormCliente,
        ItemListaClientes
    },
};
</script>

<template>
    <button @click="btnPrincipal" class="btn-cadastrar" :class="{'btn-cadastrar--cancelar': mensagemBTN === 'Cancelar'}">{{ mensagemBTN }}</button>
    <FormCliente v-if="mostrarFormulario" @cadastrar="cadastrarCliente" />
    <ul class="list">
        <li class="list_item">
            <ItemListaClientes v-for="(cliente, index) in clientes" :key="index" :cliente="cliente" @excluir-cliente="excluirClienteDoLocalStorage" />
        </li>
    </ul>
</template>