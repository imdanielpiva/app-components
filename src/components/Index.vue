<template>
  <div class="layout-padding docs-input row justify-center">
    <div style="width: 100%;">
      <q-field
        :label="route.label"
        :label-width="2"
        :helper="route.helper"
        :error="error2"
        :error-label="route.error"
      >
        <q-input v-model="route.value" :float-label="route.floatLabel" />
      </q-field>
      <q-field
        :label="streetLocation.label"
        :label-width="2"
        :helper="streetLocation.helper"
        :error="error2"
        :error-label="streetLocation.error"
        v-if="streetLocation.status"
      >
        <q-input v-model="streetLocation.value" :float-label="streetLocation.floatLabel" />
      </q-field>
      <q-field
        :label="postalCode.label"
        :label-width="2"
        :helper="postalCode.helper"
        :error="error2"
        :error-label="postalCode.error"
        v-if="postalCode.status"
      >
        <q-input v-model="postalCode.value" :float-label="postalCode.floatLabel" />
      </q-field>
      <q-field
        :label="city.label"
        :label-width="2"
        :helper="city.helper"
        :error="error2"
        :error-label="city.error"
        v-if="city.status"
      >
        <q-input v-model="city.value" :float-label="city.floatLabel" />
      </q-field>
      <q-field
        :label="state.label"
        :label-width="2"
        :helper="state.helper"
        :error="error2"
        :error-label="state.error"
        v-if="state.status"
      >
        <q-input v-model="state.value" :float-label="state.floatLabel" />
      </q-field>
      <q-field
        :label="country.label"
        :label-width="2"
        :helper="country.helper"
        :error="error2"
        :error-label="country.error"
        v-if="country.status"
      >
        <q-input v-model="country.value" :float-label="country.floatLabel" />
      </q-field>
    </div>
    <!-- <p>{{ excludeInput }}</p> -->
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
  props: {
    lang: String,
    exclude: {
      default: false
    }
  },
  data () {
    return {
      route: {
          status: '',
          value:'',
          label: 'Street Address',
          floatLabel: 'Your street address',
          helper: 'Some helper',
          error: ''
      },
      streetLocation: {
          status: true,
          value:'',
          label: 'Number Location',
          floatLabel: 'Your number location',
          helper: 'Some helper',
          error: ''
      },
      postalCode: {
          status: true,
          value:'',
          label: 'Postal Code',
          floatLabel: 'Your postal code',
          helper: 'Some helper',
          error: ''
      },
      city: {
          status: true,
          value:'',
          label: 'City',
          floatLabel: 'Your city',
          helper: 'Some helper',
          error: ''
      },
      state: {
          status: true,
          value:'',
          label: 'State',
          floatLabel: 'Your state',
          helper: 'Some helper',
          error: ''
      },
      country: {
          status: true,
          value:'',
          label: 'Country',
          floatLabel: 'Your Country',
          helper: 'Some helper',
          error: ''
      },
      error: true,
      error2: false,
      e: this.exclude
    }
  },
  computed: {
    excludeInput: function () {
      if (this.exclude) {
        switch (this.exclude) {
          case 'route':
            console.log('route')
            return;
          case 'streetLocation':
            console.log('Number Location');
            return this.streetLocation.status = false;
          case 'postalCode':
            console.log('postal code');
            return this.postalCode.status = false;
          case 'city':
            console.log('city');
            return this.city.status = false;
          case 'state':
            console.log('state');
            return this.state.status = false;
          case 'country':
            console.log('country');
            return this.country.status = false;
          case []: console.log('array');
          default:
            console.log('Falso');
            return;
        }
      }
    },

  }
}
</script>
