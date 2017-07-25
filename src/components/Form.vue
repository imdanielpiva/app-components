<template>
  <div style="width:80%; margin:auto;">
    <q-field>
       <s-test lang="br" :inline="true"></s-test>
    </q-field>
  </div>
</template>

<script>
import SAddress from './Address.vue';
import { QField } from 'quasar';

export default {
  components: {
    SAddress,
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

