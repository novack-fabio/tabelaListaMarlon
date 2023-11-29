<script>
export default {
    props: {
        tarefa: String,
        img: String,
    },
    methods: {
        marcarConcluida() {
            this.$emit('tarefa-concluida', !this.concluida);
        },
        removerTarefa() {
            this.$emit('remover-tarefa');
        },
    },
};
</script>

<template>
    <div class="tarefa">
        <v-checkbox density="compact" label="" hide-details center-affix v-bind="concluida" @change="marcarConcluida" />
        <img :src="img"/>
        <span>{{ tarefa }}</span>
        <v-icon icon="mdi-delete" @click="removerTarefa"></v-icon>
    </div>
</template>

<style scoped>
.tarefa {
    border: black solid 1px;
    border-radius: 5px;
    background-color: #efefef;
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 20%;
    margin-bottom: 10px;
}
span {
    width: 80%;
}
</style>