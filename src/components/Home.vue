<template>
    <v-app>
        <v-container>
            <v-row>
                <v-col v-for="(item, i) in items" :key="i" cols="12">
                    <v-card :color="item.color" dark shaped>
                        <v-avatar class="ma-3" size="125" tile>
                            <v-img :src=item.image></v-img>
                        </v-avatar>
                        <div class="d-flex flex-no-wrap justify-space-between">
                            <div>
                                <v-card-title class="headline" v-text="item.title"></v-card-title>
                                <v-card-subtitle v-text="item.innerText"></v-card-subtitle>
                            </div>
                        </div>
                    </v-card>
                </v-col>
                <v-col cols="12">
                    <v-card to="/search" ripple :color=thirdColor class="mx-auto" max-width="1000px" dark shaped>
                        <v-ripple>
                            <div>
                                <v-img src="@/assets/search_btn.png"></v-img>
                                <v-card-title>Click to search our registry</v-card-title>
                            </div>
                        </v-ripple>
                    </v-card>
                </v-col>
            </v-row>
            <v-container id="bottom">
                <v-btn :color=buttonColor :height=60 href="https://www.facebook.com/sultanadisastermuseummarion/">
                    <v-img contain :height=30 src="@/assets/fb.svg"></v-img>
                </v-btn>
            </v-container>
        </v-container>
    </v-app>
</template>

<script>
    export default {
        name: 'Home',

        data: () => ({
            items: [
            {
                image: '@/assets/missing_image.png',
                color: '#232F34',
                title: 'Welcome to the museum!',
                innerText: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Amet consectetur adipiscing elit ut aliquam purus sit. Sed augue lacus viverra vitae congue eu. Facilisis magna etiam tempor orci eu lobortis elementum nibh. Eu consequat ac felis donec et odio. Adipiscing elit duis tristique sollicitudin nibh. Odio eu feugiat pretium nibh ipsum consequat. Sed id semper risus in hendrerit gravida rutrum quisque non. Morbi tristique senectus et netus et malesuada. Vel pretium lectus quam id leo in vitae turpis massa. Sed odio morbi quis commodo odio aenean sed adipiscing diam. Ut lectus arcu bibendum at varius. Posuere lorem ipsum dolor sit amet consectetur adipiscing elit duis. Aliquet nibh praesent tristique magna sit. Mus mauris vitae ultricies leo integer malesuada nunc vel risus. Leo integer malesuada nunc vel.',
            },
            {
                image: '@/assets/missing_image.png',
                color: '#232F34',
                title: 'Location',
                innerText: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Amet consectetur adipiscing elit ut aliquam purus sit. Sed augue lacus viverra vitae congue eu. Facilisis magna etiam tempor orci eu lobortis elementum nibh. Eu consequat ac felis donec et odio. Adipiscing elit duis tristique sollicitudin nibh. Odio eu feugiat pretium nibh ipsum consequat. Sed id semper risus in hendrerit gravida rutrum quisque non. Morbi tristique senectus et netus et malesuada. Vel pretium lectus quam id leo in vitae turpis massa. Sed odio morbi quis commodo odio aenean sed adipiscing diam. Ut lectus arcu bibendum at varius. Posuere lorem ipsum dolor sit amet consectetur adipiscing elit duis. Aliquet nibh praesent tristique magna sit. Mus mauris vitae ultricies leo integer malesuada nunc vel risus. Leo integer malesuada nunc vel.',
            },
            ],
        }),
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
        computed: {
          getSecondaryColor() {
            return this.secondaryColor
          }
        }
    }
</script>
