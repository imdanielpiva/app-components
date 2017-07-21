<template>
  <div class="layout-padding docs-input row justify-center">
    <div style="width:100%">
      <div class="q-field row no-wrap items-start q-field-floating">
        <div class="row col">
          <div class="q-field-label col-xs-12 q-field-margin col-sm-2">
            <div class="q-field-label-inner row items-center"><span>Street Number</span></div>
          </div>
          <div class="q-field-content col-xs-12 col-sm">
            <div :class="classes.firstDiv">
              <div class="q-if-inner col row no-wrap items-center relative-position">
                <div :class="classes.secondDiv">Your street number</div>
                <input type="text" v-model="route.value" @focus="toggleClass" @blur="toggleClass" :id="id" placeholder=""  class="col q-input-target text-left">
              </div>
            </div>
            <div class="q-field-bottom row no-wrap">
              <div class="q-field-helper col">Some helper</div>
            </div>
          </div>
        </div>
      </div>
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
    <div>
      <p>{{ result }}</p>
    </div>
  </div>
</template>

<script>

import {
  QField,
  QInput,
  QBtn,
  QIcon
} from 'quasar';

export default {
  name: 's-test',
  components: {
    QField,
    QInput,
    QBtn,
    QIcon
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
  data() {
    return {
      autocomplete: '',
      types:  {
        type: String,
        default: 'geocode'
      },
      id: 'id',
      result: '',
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
      inputValue: '',
      classes: {
        firstDiv: {
          'q-if': true,
          row: true,
          'no-wrap': true,
          'items-center': true,
          'relative-position': true,
          'q-input': true,
          'q-if-has-label': true,
          'text-primary': true,
          'q-if-focused': false
        },
        secondDiv: {
          'q-if-label': true,
          ellipsis: true,
          'full-width': true,
          absolute: true,
          'self-start': true,
          'q-if-label-above': false
        }
      }
    }
  },
  mounted() {

    this.autocomplete = new google.maps.places.Autocomplete(
      document.getElementById(this.id),
      {types: ['geocode']}
    );

    this.autocomplete.addListener('place_changed', () => {
      const place = this.autocomplete.getPlace();
      console.log(place)
      // if (place) {
      //   const result = this.result = place.reduce((acc, cur, i) => {
      //     acc[i] = cur;
      //     return acc;
      //   }, {});
      //   // console.log(result);
      //   // this.route.value = result[0].long_name;
      //   // this.streetNumber.value = result[1].long_name;
      //   // this.route.value = result[0].long_name;
      //   // console.log(this.route.value);
      // }
    });


  },
  methods: {
    toggleClass: function () {
      const classes = this.classes;
      classes.firstDiv['q-if-focused'] = !classes.firstDiv['q-if-focused'];
      classes.secondDiv['q-if-label-above'] = !classes.secondDiv['q-if-label-above'];
    }
  },
  computed: {
    isEmpty: function () {
      ;
    }
  }
}
</script>

<style>
.pac-container {
  padding: 4px;
}

.pac-item {
  padding:8px;
}

.pac-container:after {
  background-image: none !important;
  padding: 0;
  height: 0px;
}
</style>
