<template>
  <div class="layout-padding docs-input row justify-center">
    <div style="width: 100%;">
      <q-field
        label="Street Address"
        :label-width="2"
        helper="Some helper"
        :error="error2"
        :error-label="route.error"
      >
        <q-input v-model="route.value" float-label="Your street Address" />
      </q-field>
      <q-field
        label="Street Number"
        :label-width="2"
        helper="Some helper"
        :error="error2"
        :error-label="streetNumber.error"
        v-if="i.streetNumber === 'streetNumber' || exclude === false"
      >
        <q-input v-model="streetNumber.value" float-label="Your street number" />
      </q-field>
      <q-field
        label="Postal Code"
        :label-width="2"
        helper="Some helper"
        :error="error2"
        :error-label="postalCode.error"
        v-if="i.postalCode === 'postalCode' || exclude === false"
      >
        <q-input v-model="postalCode.value" float-label="Your postal code" />
      </q-field>
      <q-field
        label="City"
        :label-width="2"
        helper="Some helper"
        :error="error2"
        :error-label="city.error"
        v-if="i.city === 'city' || exclude === false"
      >
        <q-input v-model="city.value" float-label="Your city" />
      </q-field>
      <q-field
        label="State"
        :label-width="2"
        helper="Some helper"
        :error="error2"
        :error-label="state.error"
        v-if="i.state === 'state' || exclude === false"
      >
        <q-input v-model="state.value" float-label="Your state" />
      </q-field>
      <q-field
        label="Country"
        :label-width="2"
        helper="Some helper"
        :error="error2"
        :error-label="country.error"
        v-if="i.country === 'country' || exclude === false"
      >
        <q-input v-model="country.value" float-label="Your Country" />
      </q-field>
    </div>
    {{ excludedInputs }}
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
    lang: {
      default: 'pt-br',
      required: false
    },
    exclude: {
      default: false,
      required: false
    },
    showIcons: {
      type: String,
      default: true,
      required: false
    }
  },
  data () {
    return {
      fields: [
        'streetNumber',
        'postalCode',
        'city',
        'state',
        'country',
        'inline'
      ],
      i:{},
      route: {
          value:'',
          error: ''
      },
      streetNumber: {
          value:'',
          error: ''
      },
      postalCode: {
          value:'',
          error: ''
      },
      city: {
          value:'',
          error: ''
      },
      state: {
          value:'',
          error: ''
      },
      country: {
          value:'',
          error: ''
      },
      error: true,
      error2: false
    }
  },
  computed: {
    excludedInputs: function () {
      const excludes = this.exclude;
      if (excludes) {
        this.i = this.fields
        .filter(field => !excludes
        .includes(field))
        .reduce(function(acc, cur, d) {
          acc[cur] = cur;
          return acc;
        }, {});
        console.log(this.i);
        return;
      }
    }
  }
}
</script>
