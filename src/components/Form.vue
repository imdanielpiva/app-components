<template>
  <div style="width:80%; margin:auto;">
    <q-field>
       <s-address lang="pt-br" :exclude="excludedInputs"></s-address>
    </q-field>
  </div>
</template>

<script>
import SAddress from './Index.vue';
import { QField } from 'quasar';

export default {
  components: {
    SAddress,
    QField
  },
  data() {
    return {
      excludedInputs: ['number-location', 'postal-code', 'city', 'state', 'country']
    }
  }
}
</script>

