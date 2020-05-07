<template>
    <v-app>
        <v-content>
            <Toolbar 
            v-bind:navButtons="navButtons" 
            v-bind:primaryColor="primaryColor"
            v-bind:secondaryColor="secondaryColor"
            v-bind:thirdColor="thirdColor"
            v-bind:buttonColor="buttonColor"
            ></Toolbar>
            <v-container fluid>
                <router-view
                v-bind:primaryColor="primaryColor"
                v-bind:secondaryColor="secondaryColor"
                v-bind:thirdColor="thirdColor"
                v-bind:buttonColor="buttonColor"></router-view>
            </v-container>
        </v-content>
        <v-footer padless app :color=thirdColor :height="60">
            <v-col class="text-center white--text" col="12">
                {{ new Date().getFullYear() }} — <strong>Sultana Museum</strong>
            </v-col>
        </v-footer>
    </v-app>
</template>

<script>
import Toolbar from "@/components/Navigation/Toolbar";

const firebase = require("firebase");
require("firebase/functions");
if(!firebase.apps.length){
    firebase.initializeApp({
    apiKey: 'AIzaSyAGrITGacZZagx9nXTYl7kLqWPpQ9AFYbM',
    authDomain: 'sultana-7f06a.firebaseapp.com',
    projectId: 'sultana-7f06a',
    databaseURL: 'https://sultana-7f06a.firebaseio.com',
    appId: '1:1005050625285:web:22295527eb8ab870ffcb6c',
    storageBucket: 'gs://sultana-7f06a.appspot.com'
  });
}

export default {
    name: "App",
    data() {
        return {
            navButtons: [
                { title: "Home", icon: "home", route: "/" },
                { title: "Search", icon: "search", route: "/search" },
                { title: "About Us", icon: "help", route: "/about" }
            ],
            primaryColor: '#344955',
            secondaryColor: '#232F34',
            thirdColor: '#4A6572',
            buttonColor: '#F9AA33'
        };
    },
    components: {
        Toolbar
    }
};
</script>
