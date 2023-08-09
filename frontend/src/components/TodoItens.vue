<template>
    <TodoSpinner v-if="loading" />
    <div class="all" v-if="users.length">
        <Panel header="USUÁRIOS" class="licitacoessty">
            <div class="card">
                <div class="flex align-items-center">
                    <span class="block">

                        <Button @click="addnovo()">
                           <icon class="pi pi-user-plus"> adicionar novo</icon> 
                        </Button>
                    </span>
                </div>
                <DataView :value="users" paginator :rows="5">
                    <template #list="slotProps">
                        <div class="col-12">
                            <div class="flex flex-column xl:flex-row xl:align-items-start p-4 gap-4">
                                <div
                                    class="flex flex-column sm:flex-row justify-content-between align-items-center xl:align-items-start flex-1 gap-4">
                                    <div class="flex flex-column align-items-center sm:align-items-start gap-3">
                                        <Image :src=slotProps.data.imagem alt="Image" width="100" />
                                        <span class="text-2xl font-bold text-900"><strong>Nome: </strong>
                                                        {{ slotProps.data.nome }} - {{ slotProps.data.username }}</span>
                                        <div class="font-semibold">Localização: {{ slotProps.data.cidade }} - {{
                                            slotProps.data.pais }}</div>
                                            <div class="font-semibold">Idade: {{ slotProps.data.idade }} </div>
                                            <div class="font-semibold">Genero: {{ slotProps.data.genero }} </div>
                                            <div class="font-semibold">Email: {{ slotProps.data.email }} </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </template>
                </DataView>
            </div>
        </Panel>
    </div>
    <TodoEmpty v-else />
</template>

<script>
import Button from 'primevue/button';
import Image from 'primevue/image';
import Panel from 'primevue/panel';
import DataView from 'primevue/dataview';
import TodoSpinner from '@/components/TodoSpinner';
import TodoEmpty from '@/components/TodoEmpty';

export default {
    name: 'App',
    components: { Button, Panel, Image, DataView, TodoSpinner, TodoEmpty },
    data() {
        return {
            users: {},
        }
    },
    methods: {

        async getUsers() {
            const req = await fetch('http://localhost:8080/all', { method: "GET", headers: { 'Content-Type': 'application/json', } })
            const data = await req.json()
            this.users = data
            console.log(this.users);
        },

        async addnovo() {
            await fetch('http://localhost:8080/new', { method: "GET", headers: { 'Content-Type': 'application/json', } })
            this.getUsers();
        },

    },
    mounted() {
        this.getUsers()
    }
}
</script>

<style>
.all {
    background-image: url('../assets/img/logo.png');
}

.licitacoessty {
    width: 80%;
    justify-content: center;
    align-content: center;
    margin-left: 10%;
}

.info {
    justify-content: center;
    align-content: right;
    margin-left: 10%;
}
</style>


    