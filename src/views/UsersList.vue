<template>
    <v-container class="ml-5">
        <v-app-bar dense color="sidebar"><h2>Meilleurs scores</h2></v-app-bar>
        <!-- LOADING ANIMATION -->
        <div v-if="loading == true">
            <v-progress-circular indeterminate size="64" color="accent"></v-progress-circular>
        </div>
        <!-- ERROR MESSAGE -->
        <div v-if="loading == false && isError == true">
            <v-alert
                dense
                border="left"
                type="error"
            >
                Oops ! Une erreur est survenue lors du chargement des scores.
                <v-btn color="warning" class="d-flex justify-end" v-on:click="loadUsersList">Réessayer</v-btn>
            </v-alert>
        </div>
        <!-- USERS LIST -->
        <div v-if="loading == false && isError == false">
            <v-alert
                dense
                border="left"
                type="success"
                dismissible
            >
                {{getUsersListSize}} score(s) récupéré(s)
            </v-alert>
            <v-list elevation="1">
                <v-layout class="d-flex">
                    <v-btn class="ma-2" color="accent" v-on:click="loadUsersList"><v-icon>mdi-reload</v-icon></v-btn>
                    <v-btn v-if="alphabeticalSort == '' || alphabeticalSort == 'descending'"  class="ma-2" color="accent" v-on:click="sortListByNameAscending"><v-icon>mdi-sort-alphabetical-ascending</v-icon></v-btn>
                    <v-btn v-if="alphabeticalSort == 'ascending'"  class="ma-2" color="accent" v-on:click="sortListByNameDescending"><v-icon>mdi-sort-alphabetical-descending</v-icon></v-btn>
                    <v-spacer/><v-spacer/><v-spacer/><v-text-field class="ma-2 justify-end" rounded filled dense placeholder="Recherche" v-model="searchTerm"></v-text-field>
                </v-layout>
                <v-list-item-group>
                    <v-list-item
                        v-for="user in filterByTerm"
                        :key="user.username"
                    >
                        <v-list-item-avatar>
                            <v-avatar>
                                <Avatar :username=user.username></Avatar>
                            </v-avatar>
                        </v-list-item-avatar>

                        <v-list-item-content>
                            <v-list-item-title v-text="user.username" :text-color='hover ? "primary" : "secondary"'></v-list-item-title>
                            <v-list-item-subtitle v-text="user.userId"></v-list-item-subtitle>
                        </v-list-item-content>

                        <v-list-item-icon>
                            <v-icon>
                                mdi-trophy-outline
                            </v-icon>
                        </v-list-item-icon>
                    </v-list-item>
                </v-list-item-group>
                <v-subheader>
                    Total : {{getFilteredUsersListSize}}
                </v-subheader>
            </v-list>
        </div>
    </v-container>
</template>

<script>
import Avatar from "vue-avatar"

const apiUrl = "https://portalz.cloud2.thibaultdct.fr"
const usersEndpoint = "/users/"

export default {
    name: "UsersList",
    components: {Avatar},

    data() {
        return {
            overlay: true,
            loading: true,
            isError: false,
            users: null,
            searchTerm: "",
            alphabeticalSort: "",
        }
    },

    methods: {
        loadUsersList: function () {
            this.users = null
            this.loading = true
            this.isError = false
            this.searchTerm = ""
            this.axios
                .get(apiUrl + usersEndpoint)
                .then(res => {
                    console.log(res)
                    this.users = res.data.users
                    this.loading = false
                })
                .catch(err => {
                    console.error(err); 
                    this.loading = false
                    this.isError = true
                })
        },
        sortListByNameAscending: function () {
            this.alphabeticalSort = 'ascending'
            this.users.sort(function(a, b) {
                return a.username[0] > b.username[0]
            })
        },
        sortListByNameDescending: function () {
            this.alphabeticalSort = 'descending'
            this.users.sort(function(a, b) {
                return a.username[0] <= b.username[0]
            })
        },
    },
    
    mounted() {
        this.loadUsersList()
    },

    computed: {
        getUsersListSize () {
            return this.users.length
        },
        getFilteredUsersListSize () {
            return this.filterByTerm.length
        },
        filterByTerm () {
            return this.users.filter(user => {
                return user.username.toLowerCase().includes(this.searchTerm.toLowerCase())
                || user.mail.toLowerCase().includes(this.searchTerm.toLowerCase())
                || user.user_id.toLowerCase().includes(this.searchTerm.toLowerCase());
            })
        },
    },

}
</script>
<style>
</style>