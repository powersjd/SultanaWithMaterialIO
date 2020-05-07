<template>
  <span>
    <SearchPeople
    v-bind:primaryColor="primaryColor"
    v-bind:secondaryColor="secondaryColor"
    v-bind:thirdColor="thirdColor"
    v-bind:buttonColor="buttonColor"
    />
  </span>
</template>

<script>
// @ is an alias to /src
import SearchPeople from '@/components/Search/SearchPeople.vue'

export default {
  name: 'Search',
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
  components: {
    SearchPeople
  }
}
</script>
