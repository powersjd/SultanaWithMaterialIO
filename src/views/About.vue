<template>
    <span>
        <AboutContent></AboutContent>
    </span>
</template>

<script>
// @ is an alias to /src
import AboutContent from '@/components/About/AboutContent.vue'

export default {
  name: 'About',
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
    AboutContent
  }
}
</script>
