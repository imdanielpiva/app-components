<template>
  <div style="width:80%; margin:auto;">
    <q-field>
       <s-test lang="br"></s-test>
    </q-field>
  </div>
</template>

<script>
import Test from './Test.vue';
import { QField } from 'quasar';

export default {
  components: {
    Test,
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

