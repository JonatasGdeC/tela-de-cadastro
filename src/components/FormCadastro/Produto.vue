<script>
import './styles.scss'

export default { 
    data() {
        return {
            nome: '',
        }
    },
    methods: {
        cadastrar() {
            const dadosProduto = {
                nome: this.nome
            }

        const verificando = () => {
            this.nome.length < 3 ? alert('O nome do produto deve ter no mínimo 3 caracteres...') : this.$emit('cadastrar', dadosProduto);
            }
        verificando()
        },
    }
}
</script>

<template>
    <div class="form">
        <form>
            <div class="form_campo">
                <label class="form_campo_nome" for="nome">Nome do Produto:</label>
                <input class="form_campo_input" v-model="nome" type="text" id="nome">
            </div>
        </form>
        <button class="form_button" @click="cadastrar">Cadastrar</button>
    </div>
</template>