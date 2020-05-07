<template>
    <nav>
        <v-app-bar :color=primaryColor app dark>
            <div class="d-flex align-center">
                <router-link to="/">
                    <v-img
                        alt="Sultana Logo"
                        class="shrink mr-2 hidden-md-and-down"
                        contain
                        src="@/assets/logo.png"
                        transition="scale-transition"
                        width="80"
                    />
                </router-link>
            </div>
            <v-spacer class="hidden-md-and-down"></v-spacer>
            <v-app-bar-nav-icon class="hidden-lg-and-up" right @click="drawer = !drawer"></v-app-bar-nav-icon>
            <v-btn right class="hidden-md-and-down" v-for="(item, index) in this.navButtons" :key="index" :to="item.route" text>
                {{ item.title }}
                <v-icon :key="index" class="material-icons ml-2">{{ item.icon }}</v-icon>
            </v-btn>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" :color=secondaryColor absolute dark>
            <v-list shaped dense nav class="py-0">
                <v-list-item two-line>
                    <v-list-item-content>
                        <v-list-item-title>Site Navigation</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>

                <v-divider></v-divider>

                <v-list-item v-for="item in this.navButtons" :key="item.title" :to="item.route" link>
                    <v-list-item-icon>
                        <v-icon class="material-icons">{{ item.icon }}</v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>

    </nav>

</template>


<script>

export default {
    name: 'TopBar',

    data() {
        return {
            drawer: false
        }
    },

    props: {
        navButtons: {
            type: Array
        },
        primaryColor: {
            type: String
        },
        secondaryColor: {
            type: String
        },
        thirdColor: {
            type: String
        },
        buttonColor: {
            type: String
        }
    },
};
</script>