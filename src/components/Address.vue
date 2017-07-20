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
        <q-input
          v-model="autocompleteText"
          float-label="Your street Address"
          @input="getAddressData"
        />
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
      <input
        type="text"
        v-model="autocompleteText"
      >
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
      default: 'br',
      required: false
    },
    exclude: {
      default: false,
      required: false
    },
    showIcons: {
      type: Boolean,
      default: true,
      required: false
    },
    inline: {
      type: Boolean,
      default: false,
      required: false
    },
    changed: {
      type: String,
      default: 'getAddressData'
    }
  },

  data () {
    return {
      fields: [
        'streetNumber',
        'postalCode',
        'city',
        'state',
        'country'
      ],
      i:{},
      route: {
          value:''
      },
      streetNumber: {
          value:''
      },
      postalCode: {
          value:''
      },
      city: {
          value:''
      },
      state: {
          value:''
      },
      country: {
          value:''
      },
      error: true,
      error2: false,
      autocomplete: '',
      autocompleteText: ''
    }
  },
  mounted() {

    const options = {
      types: [this.types]
    };

    if (this.lang) {
      options.componentRestrictions = {
        country: this.lang
      };
    }

    this.autocomplete = new google.maps.places.Autocomplete(
      document.getElementById(this.id),
      options
    );

    console.log(this.autocomplete);

    console.log(this.autocomplete.addListener('place_changed', () => {
      let place = this.autocomplete.getPlace();

      if (!place.geometry) {
        // User entered the name of a Place that was not suggested and
        // pressed the Enter key, or the Place Details request failed.
        this.$emit('no-results-found', place);
        return;
      }

      let addressComponents = {
        street_number: 'short_name',
        route: 'long_name',
        locality: 'long_name',
        administrative_area_level_1: 'short_name',
        country: 'long_name',
        postal_code: 'short_name'
      };

      console.log(addressComponents + 'address components')

      let returnData = {};

      if (place.address_components !== undefined) {
        // Get each component of the address from the place details
        for (let i = 0; i < place.address_components.length; i++) {
          let addressType = place.address_components[i].types[0];
          if (addressComponents[addressType]) {
            let val = place.address_components[i][addressComponents[addressType]];
              returnData[addressType] = val;
          }
        }
        returnData['latitude'] = place.geometry.location.lat();
        returnData['longitude'] = place.geometry.location.lng();
        // return returnData object and PlaceResult object
        // this.$emit('placechanged', returnData, place, this.id);
        this.$emit('changed', returnData, place);
      }
    }));
  },
  methods: {
    getAddressData: function (addressData, placeResultData) {
      this.address = addressData;
      console.log(this.address);
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
