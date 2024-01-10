<script>
import './styles.scss'
</script>

<template>
    <div class="form">
        <form>
            <div class="form_campo">
                <label class="form_campo_nome" for="nome">Nome do Produto:</label>
                <input class="form_campo_input" type="text" id="nome">
            </div>
            <div class="form_campo">
                <label class="form_campo_nome" for="ativo">Ativo?</label>
                <select class="form_campo_input" id="ativo">
                    <option>Sim</option>
                    <option>Não</option>
                </select>
            </div>
        </form>
        <button class="form_button">Cadastrar</button>
    </div>
</template>