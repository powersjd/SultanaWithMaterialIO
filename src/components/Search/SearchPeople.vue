<template>
    <v-app>
        <v-layout column align-center>
            <v-card class="mb-2" :width=1000 outlined :color=thirdColor dark>
                <v-card-title class="title">
                    Welcome to the directory search!
                </v-card-title>
                <v-card-subtitle class="headline">
                    To use, choose a table below and enter the information in the search fields.  When you are done searching, click "Press to Search" to search.
                </v-card-subtitle>
            </v-card>
            <v-card :width=2000 class="ml-2 mr-2" outlined :color=secondaryColor dark>
                <v-card-title primary-title class="justify-center ml-2">
                    Liberated Soldiers Search
                    <v-spacer></v-spacer>
                    <v-text-field 
                    :color=buttonColor
                    v-model="prisonerFirstName" 
                    v-on:keyup.enter="searchPrisoners" 
                    label="First Name" 
                    single-line />
                    <v-text-field 
                    :color=buttonColor
                    v-model="prisonerLastName" 
                    v-on:keyup.enter="searchPrisoners" 
                    label="Last Name" 
                    single-line/>
                    <v-select 
                    :color=buttonColor
                    v-model="prisonerState" 
                    :items="stateSelect" 
                    placeholder="State"/>
                    <v-select
                    :color=buttonColor
                    v-model="prisonerCompany" 
                    :items="companySelect" 
                    placeholder="Company"/>
                    <v-select
                    :color=buttonColor
                    v-model="prisonerPrison" 
                    :items="prisonSelect" 
                    placeholder="Prison"/>
                </v-card-title>
                <v-data-table 
                @click:row="handlePrisonClick"
                :headers="prisonHeaders" 
                :items="searchedPrisoners" 
                :items-per-page="10"
                class="elevation-1"
                single-select
                :must-sort="true"
                sort-by="lastname"
                :loading="prisonersLoading"
                loading-text="Loading... Please Wait"/>
                <v-btn @click="searchPrisoners()" x-large height="50px" text :color=buttonColor>Press to search</v-btn>
            </v-card>

            <v-card :width=2000 class="ml-2 mt-2 mr-2" outlined :color=secondaryColor dark>
                <v-card-title primary-title class="justify-center ml-2">
                    Crew Search
                    <v-spacer></v-spacer>
                    <v-text-field 
                    :color=buttonColor
                    v-model="crewFirstName" 
                    v-on:keyup.enter="searchOhio" 
                    label="First Name" 
                    single-line />
                    <v-text-field 
                    :color=buttonColor
                    v-model="crewLastName" 
                    v-on:keyup.enter="searchOhio" 
                    label="Last Name" 
                    single-line/>
                    <v-select
                    :color=buttonColor
                    v-model="crewCompany" 
                    :items="companySelect" 
                    placeholder="Company"/>
                </v-card-title>
                <v-data-table 
                @click:row="handleCrewClick"
                :headers="ohioHeaders" 
                :items="searchedOhio" 
                :items-per-page="10"
                class="elevation-1"
                single-select
                :must-sort="true"
                sort-by="lastname"
                :loading="crewLoading"
                loading-text="Loading... Please Wait"/>
                <v-btn @click="searchOhio()" x-large height="50px" text :color=buttonColor>Press to search</v-btn>
            </v-card>

            <v-card :width=2000 class="ml-2 mt-2 mr-2" outlined :color=secondaryColor dark>
                <v-card-title primary-title class="justify-center ml-2">
                    Passengers Search
                    <v-spacer></v-spacer>
                    <v-text-field 
                    :color=buttonColor
                    v-model="passengerFirstName" 
                    v-on:keyup.enter="searchPassengers" 
                    label="First Name" 
                    single-line />
                    <v-text-field 
                    :color=buttonColor
                    v-model="passengerLastName" 
                    v-on:keyup.enter="searchPassengers" 
                    label="Last Name" 
                    single-line/>
                </v-card-title>
                <v-data-table 
                @click:row="handlePassengerClick"
                :headers="passengerHeaders" 
                :items="searchedPassengers" 
                :items-per-page="10"
                class="elevation-1"
                single-select
                :must-sort="true"
                sort-by="lastname"
                :loading="passengersLoading"
                loading-text="Loading... Please Wait"/>
                <v-btn @click="searchPassengers()" x-large height="50px" text :color=buttonColor>Press to search</v-btn>
            </v-card>
        </v-layout>
        

        <v-dialog v-model="prisonerDialog" max-width="800">
            <v-card :color=primaryColor dark outlined>
                <v-card-title class="headline">{{ this.dialogData['firstname'] + " " + this.dialogData['lastname'] }}</v-card-title>

                <v-card-text>
                    <strong>First Name: {{ this.dialogData['firstname'] }} </strong>
                    <v-spacer></v-spacer>
                    <strong>Last Name: {{ this.dialogData['lastname'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Age: {{ this.dialogData['age'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Fate: {{ this.dialogData['fate'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>State: {{ this.dialogData['state'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Company: {{ this.dialogData['company'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Regiment: {{ this.dialogData['regiment'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Rank: {{ this.dialogData['rank'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Prison: {{ this.dialogData['prison'] }}</strong>
                    <v-spacer></v-spacer>
                    <v-container fluid>
                        <v-row align='center' justify='center'>
                            <v-spacer></v-spacer>
                            <img :src='imageOneLink' height="200"/>
                            <v-spacer></v-spacer>
                            <img :src='imageTwoLink' height="200"/>
                            <v-spacer></v-spacer>
                        </v-row>
                    </v-container>
                    <v-spacer></v-spacer>
                    <strong>Sources: {{ this.dialogData['comments'] }}</strong>

                </v-card-text>

                <v-card-actions>
                    <v-btn :color=buttonColor text @click="prisonerDialog = false">Close</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>

        <v-dialog v-model="crewDialog" max-width="800">
            <v-card :color=primaryColor dark outlined>
                <v-card-title class="headline">{{ this.dialogData['firstname'] + " " + this.dialogData['lastname'] }}</v-card-title>

                <v-card-text>
                    <strong>First Name: {{ this.dialogData['firstname'] }} </strong>
                    <v-spacer></v-spacer>
                    <strong>Last Name: {{ this.dialogData['lastname'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Age: {{ this.dialogData['age'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Fate: {{ this.dialogData['fate'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>State: {{ this.dialogData['state'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Company: {{ this.dialogData['company'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Regiment: {{ this.dialogData['regiment'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Rank: {{ this.dialogData['rank'] }}</strong>
                    <v-spacer></v-spacer>
                    <v-container fluid>
                        <v-row align='center' justify='center'>
                            <v-spacer></v-spacer>
                            <img :src='imageOneLink' height="200"/>
                            <v-spacer></v-spacer>
                            <img :src='imageTwoLink' height="200"/>
                            <v-spacer></v-spacer>
                        </v-row>
                    </v-container>
                    <v-spacer></v-spacer>
                    <strong>Sources: {{ this.dialogData['comments'] }}</strong>

                </v-card-text>

                <v-card-actions>
                    <v-btn :color=buttonColor text @click="crewDialog = false">Close</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>

        <v-dialog v-model="passengerDialog" max-width="800">
            <v-card :color=primaryColor dark outlined>
                <v-card-title class="headline">{{ this.dialogData['firstname'] + " " + this.dialogData['lastname'] }}</v-card-title>

                <v-card-text>
                    <strong>First Name: {{ this.dialogData['firstname'] }} </strong>
                    <v-spacer></v-spacer>
                    <strong>Last Name: {{ this.dialogData['lastname'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Age: {{ this.dialogData['age'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Fate: {{ this.dialogData['fate'] }}</strong>
                    <v-spacer></v-spacer>
                    <strong>Classification: {{ this.dialogData['classification'] }}</strong>
                    <v-spacer></v-spacer>
                    <v-container fluid>
                        <v-row align='center' justify='center'>
                            <v-spacer></v-spacer>
                            <img :src='imageOneLink' height="200"/>
                            <v-spacer></v-spacer>
                            <img :src='imageTwoLink' height="200"/>
                            <v-spacer></v-spacer>
                        </v-row>
                    </v-container>
                    <v-spacer></v-spacer>
                    <strong>Sources: {{ this.dialogData['comments'] }}</strong>

                </v-card-text>

                <v-card-actions>
                    <v-btn :color=buttonColor text @click="passengerDialog = false">Close</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </v-app>
</template>

<script>
import firebase from 'firebase';

export default {
    methods: {

        filterPassengers: function() {
            let tempArray = []
            for(let i = 0; i < this.searchedPassengers.length; i++){
                let currentEntry = this.searchedPassengers[i]
                if(this.passengerFirstName == 0 || String(currentEntry.firstname).toLowerCase() == this.passengerFirstName.toLowerCase()) {
                    if(this.passengerLastName == 0 || String(currentEntry.lastname).toLowerCase() == this.passengerLastName.toLowerCase()) {
                        tempArray.push(currentEntry)
                    }
                }
            }
            this.passengerFirstName = ""
            this.passengerLastName = ""
            this.searchedPassengers = tempArray
        },
        filterCrew: function() {
            let tempArray = []
            for(let i = 0; i < this.searchedOhio.length; i++){
                let currentEntry = this.searchedOhio[i]
                if(this.crewFirstName == 0 || String(currentEntry.firstname).toLowerCase() == this.crewFirstName.toLowerCase()) {
                    if(this.crewLastName == 0 || String(currentEntry.lastname).toLowerCase() == this.crewLastName.toLowerCase()) {
                        if(this.crewCompany == 0 || String(currentEntry.company).toLowerCase() == this.crewCompany.toLowerCase()) {
                            tempArray.push(currentEntry)
                        }
                    }
                }
            }
            this.crewFirstName = ""
            this.crewLastName = ""
            this.crewCompany = ""
            this.searchedOhio = tempArray
        },
        filterPrisoners: function() {
            let tempArray = []
            for(let i = 0; i < this.searchedPrisoners.length; i++){
                let currentEntry = this.searchedPrisoners[i]
                if(this.prisonerFirstName == 0 || String(currentEntry.firstname).toLowerCase() == this.prisonerFirstName.toLowerCase()) {
                    if(this.prisonerLastName == 0 || String(currentEntry.lastname).toLowerCase() == this.prisonerLastName.toLowerCase()) {
                        if(this.prisonerCompany == 0 || String(currentEntry.company).toLowerCase() == this.prisonerCompany.toLowerCase()) {
                            if(this.prisonerState == 0 || String(currentEntry.state).toLowerCase() == this.prisonerState.toLowerCase()) {
                                if(this.prisonerPrison == 0 || String(currentEntry.prison).toLowerCase() == this.prisonerPrison.toLowerCase()) {
                                    tempArray.push(currentEntry)
                                }
                            }
                        }
                    }
                }
            }
            this.prisonerFirstName = ""
            this.prisonerLastName = ""
            this.prisonerCompany = ""
            this.prisonerState = ""
            this.prisonerPrison = ""
            this.searchedPrisoners = tempArray
        },

        handlePrisonClick: function(event) {
            this.prisonerDialog = true
            this.dialogData = event
            this.imageOneLink = "https://firebasestorage.googleapis.com/v0/b/sultana-7f06a.appspot.com/o/pictures%2Fmissing_image.png?alt=media&token=31b8b51a-002e-4337-ae13-afbd63e095ee"
            this.imageTwoLink = "https://firebasestorage.googleapis.com/v0/b/sultana-7f06a.appspot.com/o/pictures%2Fmissing_image.png?alt=media&token=31b8b51a-002e-4337-ae13-afbd63e095ee"
            if(this.dialogData['imageOneLink'] != null && this.dialogData['imageOneLink'].length > 0) {
                this.imageOneLink = this.dialogData['imageOneLink']
            }
            if(this.dialogData['imageTwoLink'] != null && this.dialogData['imageTwoLink'].length > 0) {
                this.imageTwoLink = this.dialogData['imageTwoLink']
            }
        },
        handlePassengerClick: function(event) {
            this.passengerDialog = true
            this.dialogData = event
            this.imageOneLink = "https://firebasestorage.googleapis.com/v0/b/sultana-7f06a.appspot.com/o/pictures%2Fmissing_image.png?alt=media&token=31b8b51a-002e-4337-ae13-afbd63e095ee"
            this.imageTwoLink = "https://firebasestorage.googleapis.com/v0/b/sultana-7f06a.appspot.com/o/pictures%2Fmissing_image.png?alt=media&token=31b8b51a-002e-4337-ae13-afbd63e095ee"
            if(this.dialogData['imageOneLink'] != null && this.dialogData['imageOneLink'].length > 0) {
                this.imageOneLink = this.dialogData['imageOneLink']
            }
            if(this.dialogData['imageTwoLink'] != null && this.dialogData['imageTwoLink'].length > 0) {
                this.imageTwoLink = this.dialogData['imageTwoLink']
            }
        },
        handleCrewClick: function(event) {
            this.crewDialog = true
            this.dialogData = event
            this.imageOneLink = "https://firebasestorage.googleapis.com/v0/b/sultana-7f06a.appspot.com/o/pictures%2Fmissing_image.png?alt=media&token=31b8b51a-002e-4337-ae13-afbd63e095ee"
            this.imageTwoLink = "https://firebasestorage.googleapis.com/v0/b/sultana-7f06a.appspot.com/o/pictures%2Fmissing_image.png?alt=media&token=31b8b51a-002e-4337-ae13-afbd63e095ee"
            if(this.dialogData['imageOneLink'] != null && this.dialogData['imageOneLink'].length > 0) {
                this.imageOneLink = this.dialogData['imageOneLink']
            }
            if(this.dialogData['imageTwoLink'] != null && this.dialogData['imageTwoLink'].length > 0) {
                this.imageTwoLink = this.dialogData['imageTwoLink']
            }
        },
        searchPrisoners: async function() {
            if(this.prisoners.length == 0){
                await this.getPrisoners()
                this.searchedPrisoners = this.prisoners
            }else{
                this.searchedPrisoners = this.prisoners
            }
            this.filterPrisoners()
        },
        searchPassengers: async function() {
            if(this.passengers.length == 0){
                await this.getPassengers()
                this.searchedPassengers = this.passengers
            }else{
                this.searchedPassengers = this.passengers
            }
            this.filterPassengers()
        },
        searchOhio: async function() {
            if(this.ohio.length == 0){
                await this.getOhio()
                this.searchedOhio = this.ohio
            }else{
                this.searchedOhio = this.ohio
            }
            this.filterCrew()
        },
        getPrisoners: async function () {
            this.prisonersLoading = true;

            var getAllPeople = firebase.functions().httpsCallable('getAllPrisoner');
            await getAllPeople({
                entrynum: this.search,
            })
            .then(response => {
                response.data.forEach(doc => {
                    this.prisoners.push(doc);
                });
                this.prisonersLoading = false
            })
        },
        getPassengers: async function () {
            this.passengersLoading = true;

            var getAllPeople = firebase.functions().httpsCallable('getAllPassenger');
            await getAllPeople({
                entrynum: this.search,
            })
            .then(response => {
                response.data.forEach(doc => {
                    this.passengers.push(doc);
                });
                this.passengersLoading = false
            })
        },

        getOhio: async function () {
            this.crewLoading = true;

            var getAllPeople = firebase.functions().httpsCallable('getAllOhio');
            await getAllPeople({
                entrynum: this.search,
            })
            .then(response => {
                response.data.forEach(doc => {
                    this.ohio.push(doc);
                });
                this.crewLoading = false
            })
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
    name: 'ViewPerson',
    data: () => ({
        imageOneLink: "",
        imageTwoLink: "",
        passengerFirstName: "",
        passengerLastName: "",
        crewFirstName: "",
        crewLastName: "",
        crewCompany: "",
        prisonerFirstName: "",
        prisonerLastName: "",
        prisonerState: "",
        prisonerCompany: "",
        prisonerPrison: "",
        prisonersLoading: false,
        passengersLoading: false,
        crewLoading: false,
        prisonerDialog: false,
        crewDialog: false,
        passengerDialog: false,
        dialogData: {},
        searchedPrisoners: [],
        prisoners: [],
        searchedOhio: [],
        ohio: [],
        searchedPassengers: [],
        passengers: [],
        headers: [],
        stateSelect: [
        "Passenger",
        "Crew",
        "Guard - 58th Ohio Infantry",
        "Iowa Cavalry",
        "Illinois Infantry",
        "Indiana Artillery Battery",
        "Indiana Cavalry",
        "Indiana Infantry",
        "Kentucky Cavalry",
        "Kentucky Infantry",
        "Kentucky Light Artillery",
        "Kentucky Mounted Infantry",
        "Michigan Cavalry",
        "Michigan Engineers & Mechanics",
        "Michigan Infantry",
        "Michigan Light Artillery",
        "Michigan Sharpshooters",
        "New York Infantry",
        "Ohio Cavalry (McLaughlin)",
        "Ohio Cavalry",
        "Ohio Infantry",
        "Ohio Light Artillery",
        "Pennsylvania Cavalry",
        "Tennessee Cavalry",
        "Tennessee Infantry",
        "Tennessee Mounted Infantry",
        "United States Colored Troops",
        "Virginia (Louden County Virginia Rangers)",
        "West Virginia Cavalry",
        "West Virginia Infantry",
        "West Virginia Light Artillery"
    ],
    typeSelect: [
        'Passengers',
        'Crew',
        'Liberated Soldiers'
    ],

    companySelect: [
        "F & S (Field and Staff)",
        "A",
        "B",
        "C",
        "D",
        "E",
        "F",
        "G",
        "H",
        "I",
        "J",
        "K",
        "L",
        "M"
    ],
    prisonSelect: [
        "Andersonville, GA",
        "Cahaba. AL",
        "City Jail, Eutaw, AL",
        "Macon, GA",
        "Marion, AL",
        "Meridian, MS",
        "Millen, GA",
        "Unknown",
        "N/A"
    ],
    passengerHeaders: [
        {
            text: 'Fate',
            align: 'center',
            sortable: true,
            value: 'fate'
        },
        {
            text: 'Last Name',
            align: 'center',
            sortable: true,
            value: 'lastname'
        },
        {
            text: 'First Name',
            align: 'center',
            sortable: true,
            value: 'firstname'
        },
        {
            text: 'Age',
            align: 'center',
            sortable: true,
            value: 'age'
        },
        {
            text: 'Classification',
            align: 'center',
            sortable: 'true',
            value: 'classification'
        }
    ],
    ohioHeaders: [
        {
            text: 'Fate',
            align: 'center',
            sortable: true,
            value: 'fate'
        },
        {
            text: 'Last Name',
            align: 'center',
            sortable: true,
            value: 'lastname'
        },
        {
            text: 'First Name',
            align: 'center',
            sortable: true,
            value: 'firstname'
        },
        {
            text: 'Age',
            align: 'center',
            sortable: true,
            value: 'age'
        },
        {
            text: 'State',
            align: 'center',
            sortable: true,
            value: 'state'
        },
        {
            text: 'Regiment',
            align: 'center',
            sortable: true,
            value: 'regiment'
        },
        {
            text: 'Company',
            align: 'center',
            sortable: true,
            value: 'company'
        },
        {
            text: 'Rank',
            align: 'center',
            sortable: true,
            value: 'rank'
        }
    ],
    prisonHeaders: [
        {
            text: 'Fate',
            align: 'center',
            sortable: true,
            value: 'fate'
        },
        {
            text: 'Last Name',
            align: 'center',
            sortable: true,
            value: 'lastname'
        },
        {
            text: 'First Name',
            align: 'center',
            sortable: true,
            value: 'firstname'
        },
        {
            text: 'State',
            align: 'center',
            sortable: true,
            value: 'state'
        },
        {
            text: 'Regiment',
            align: 'center',
            sortable: true,
            value: 'regiment'
        },
        {
            text: 'Company',
            align: 'center',
            sortable: true,
            value: 'company'
        },
        {
            text: 'Rank',
            align: 'center',
            sortable: true,
            value: 'rank'
        },
        {
            text: 'Age',
            align: 'center',
            sortable: true,
            value: 'age'
        },
        {
            text: 'Prison',
            align: 'center',
            sortable: true,
            value: 'prison'
        }
    ],
})
}
</script>
