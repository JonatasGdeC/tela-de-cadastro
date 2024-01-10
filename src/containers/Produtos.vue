<script>
import './styles.scss'
import FormProduto from '../components/FormCadastro/Produto.vue'

export default {
    data(){
        return{
            mostrarFormulario: false,
            mensagemBTN: 'Cadastrar'
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
        }
    },
    components: {
        FormProduto
    }
}
</script>

<template>
    <button @click="btnPrincipal" class="btn-cadastrar" :class="{'btn-cadastrar--cancelar': mensagemBTN === 'Cancelar'}">{{ mensagemBTN }}</button>
    <FormProduto v-if="mostrarFormulario" />
</template>