<script>
export default {
    data() {
        return {
            novaTarefa: '',
        };
    },
    methods: {
        adicionarTarefa() {
            if (this.novaTarefa.trim() !== '') {
                this.$emit('tarefa-adicionada', this.novaTarefa);
                this.novaTarefa = '';
            }
        },
    },
};
</script>

<template>
    <v-text-field class="input" v-model="novaTarefa" @keyup.enter="adicionarTarefa" placeholder="Escreva o número do Pokemon" />
</template>

<style scoped>
    .input {
        height: 50px;
    }
</style>