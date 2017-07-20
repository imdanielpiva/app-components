<template>
  <div style="width:80%; margin:auto;">
    <q-field>
       <s-address lang="br"></s-address>
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
    getAddressData: function (addressData, placeResultData) {
      this.address = addressData;
      console.log(this.address);
    }
  }
}
</script>

