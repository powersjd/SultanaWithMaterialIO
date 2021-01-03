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
                innerText: 'The Sultana Disaster Museum, located in Marion, Arkansas, across the Mississippi River from Memphis, TN, was opened in 2015 and is dedicated to the memory of the greatest maritime disaster in United States history. The sidewheel steamboat Sultana exploded her boilers on the Mississippi River some seven miles above Memphis in the early morning hours of April 27, 1865. Legally registered to carry 376 passengers and a crew of around 80-85, the boat was grossly overcrowded and carrying 2,136 people when she exploded. Some 1,169 individuals lost their lives in the disaster, most being recently released Union prisoners-of-war. The museum contains many artifacts related to the disaster, to the Sultana Survivor’s Association, and to the memory of the disaster through the years. Contained within the museum are a handful of actual pieces recovered from the ill-fated Sultana.
	This database has been created so that you can search for any person that was on the Sultana from April 24, 1865, when she was overloaded at Vicksburg, MS, until April 27, 1865, when her boilers exploded above Memphis, TN. All the names found in the database – paroled Union prisoners, guard unit, passengers, and crew – have been verified to have been on board the Sultana during this time period through hundreds of sources. These sources can be seen by clicking on any individual name after obtaining your search results. For more information on any individual, please feel free to contact the Sultana Disaster Museum.',
            },
            {
                image: '@/assets/missing_image.png',
                color: '#232F34',
                title: 'Location',
                innerText: 'The interim Sultana Disaster Museum is located at 104 Washington St. in Marion, Arkansas. A permanent location, situated on the north side of E. Military Road, between Briarwood Street and Currie Avenue, has already been purchased. The new facility will be located in a 15,000 square-foot brick building built in 1938. Architects are currently working on the design of a state-of-the-art facility with plans to open in April 2023.',
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
