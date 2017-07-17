<template>
  <div class="layout-padding docs-input row justify-center">
    <div style="width: 100%;">
      <q-field
        label="Street Address"
        helper="Your street address"
        :error="error2"
        error-label="Some error"
      >
        <q-input v-model="text" />        
      </q-field>
      <q-field
        label="Number Location"
        helper="Your number location"
        :error="error2"
        error-label="Some error"
      >
        <q-input v-model="text" />        
      </q-field>
      <q-field
        label="Postal Code"
        helper="Your postal code"
        :error="error2"
        error-label="Some error"
      >
        <q-input v-model="text" />        
      </q-field>
      <q-field
        label="City"
        helper="Your city"
        :error="error2"
        error-label="Some error"
      >
        <q-input v-model="text" />        
      </q-field>
      <q-field
        label="State"
        helper="Your state"
        :error="error2"
        error-label="Some error"
      >
        <q-input v-model="text" />        
      </q-field>
      <q-field
        label="Country"
        helper="Your country"
        :error="error2"
        error-label="Some error"
      >
        <q-input v-model="text" />        
      </q-field>
    </div>
  </div>
</template>

<script>
import {
  QInput,
  QIcon,
  QField
} from 'quasar';
export default {
  name: 's-address',
  components: {
    QInput,
    QIcon,
    QField
  },
  data () {
    return {
      text: '',
      error: true,
      error2: false,
      loading: true
    }
  }
}
</script>