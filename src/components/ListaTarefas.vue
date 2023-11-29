<script>
import CampoDeInput from './CampoDeInput.vue';
import Tarefa from './Tarefa.vue';
import axios from 'axios';

export default {
    components: {
        CampoDeInput,
        Tarefa,
    },
    data() {
        return {
            tarefas: [],
        };
    },
    methods: {
        async adicionarTarefa(novaTarefa) {
            if (novaTarefa.trim() !== '') {
                const pokemon = await this.getPokemon(novaTarefa);
                this.tarefas.push({ nome: pokemon.name, img: pokemon.sprites.front_default });
            }
        },
        async getPokemon(pokemonName) {
            return axios.get(`https://pokeapi.co/api/v2/pokemon/${pokemonName}`).then((response) => {
                return response.data;
            }).catch((error) => {
                console.error(error);
            });
        },
        atualizarConclusao(index, concluida) {
            this.tarefas[index].concluida = concluida;
        },
        removerTarefa(index) {
            this.tarefas.splice(index, 1);
        },
    },
};
</script>

<template>
    <div class="body">
        <h2>Checklist de Pokemons</h2>
        <campo-de-input class="input" @tarefa-adicionada="adicionarTarefa"></campo-de-input>
        <div class="tarefas">
            <tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa.nome" :img="tarefa.img"
                @tarefa-concluida="atualizarConclusao(index, $event)" @remover-tarefa="removerTarefa(index)"></tarefa>
        </div>
    </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
h2 {
    font-family: "Press Start 2P";
}

    .body {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .input {
        width: 30%;
    }
    .tarefas {
        margin-top: 20px;
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 100%;
    }
</style>