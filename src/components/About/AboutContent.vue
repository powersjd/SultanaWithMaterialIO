<template>
    <v-container class="about">
        <v-card color="#4A6572" class="pa-2" dark>
            <v-container>
                <v-container class="row">
                    <v-container class="columnSmall">
                        <v-container class="about-container">
                            <v-img contain :height=300 src="@/assets/main_feature.png"/>
                        </v-container>
                    </v-container>
                    <v-container class="columnLarge">
                        <h1>The Disaster</h1>
                        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
                    </v-container>
                </v-container>
            </v-container>


            <v-container class="row">
                <v-container class="columnLarge ml-6">
                    <h1>Our Goal</h1>
                    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
                </v-container>
                <v-container class="columnSmall">
                    <v-container class="about-container">
                        <img src="../../assets/about2.jpg">
                    </v-container>
                </v-container>
            </v-container>
        </v-card>
    </v-container>
</template>

<script>
    export default {
        name: "About"
    }
</script>

<style scoped>

    .columnLarge h1{
        margin-top: 0;
    }

    .about-container{
        height: auto;
        max-width: 350px;
        padding: 0;
    }

    .columnLarge{
    float: left;
    width: 60%;
    padding: 0;
  }

  .columnSmall{
    float: left;
    width: 30%;
    padding: 0;
  }

  @media screen and (max-width: 800px){
    .columnLarge, .columnSmall{
      width: 100%;
      margin: 0;
    }

    .columnLarge:last-child, .columnSmall:last-child{
      margin-left: 0;
    }

    .mobile-view{
      display: block;
    }

    .desktop-view{
      display: none;
    }

    #content-container{
      width: 90%;
    }

    #fb, #bottom-buttons, #bottom-buttons > *{
      width: 100%;
      height: auto;
      min-height: 60px;
      margin: 15px auto;
        float: none;
    }

    #fb{
        width: 50%;
    }

  }

  .desktop-view{
      margin: 0 !important;
      padding: 0;
  }

  @media screen and (min-width: 800px) {

    .mobile-view{
      display: none;
    }

    .desktop-view{
      display: block;
    }

  }
  .row{
    margin-top: 20px;
    padding: 0;
    min-width: 100%;
  }
  .row:after{
    content: "";
    display: table;
    clear: both;
  }

  .mobile-menu {
    background-color: rgb(40, 51, 67) !important;
    list-style-type: none;
    /*margin-left: 25px;*/
    margin: 0 3%;
  }

  .mobile-menu > *{
    text-decoration: none;
    display: block;
    margin: 15px 0;
    /*padding: 15px 0;*/
    height: 60px !important;
    width: 100%;
  }

  .mobile-menu > * > *{
    font-size: 24px;
  }

</style>