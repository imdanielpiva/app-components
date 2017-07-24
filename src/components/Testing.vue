<template>
  <div style="width:80%; margin:auto;">
    <q-field>
       <s-test lang="br" :inline="true" :exclude="naoquero"></s-test>
    </q-field>
  </div>
</template>

<script>
import STest from './Test.vue';
import { QField } from 'quasar';

export default {
  components: {
    STest,
    QField
  },
  data() {
    return {
      state: 'parana',
      naoquero: [
        'country',
        'postalCode',
        'city'
      ]
    }
  },
  methods: {
  }
}
</script>

