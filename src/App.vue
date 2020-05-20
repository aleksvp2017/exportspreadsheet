<template>
  <v-app>
    <simpletable/>
  </v-app>
</template>

<script>
import SimpleTable from './views/SimpleTable.vue'

export default {
    components: {
      'simpletable': SimpleTable
    }, 
}
</script>
