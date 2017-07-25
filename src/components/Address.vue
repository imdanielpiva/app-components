<template>
    <div>
    <div class="layout-padding docs-input row justify-center">
      <div style="width:100%">
        <div class="q-field row no-wrap items-start q-field-floating">
          <i aria-hidden="true" class="q-field-icon q-field-margin q-icon material-icons">place</i>
          <div class="row col">
            <div class="q-field-label col-xs-12 q-field-margin col-sm-2">
              <div class="q-field-label-inner row items-center">
                <span>Street Address</span>
              </div>
            </div>
            <div class="q-field-content col-xs-12 col-sm">
              <div :class="classes.firstDiv">
                <div class="q-if-inner col row no-wrap items-center relative-position">
                  <div :class="classes.secondDiv">Your street number</div>
                  <input type="text" v-model="route.value" @focus="toggleClass" @blur="toggleClass" :id="id" placeholder=""  class="col q-input-target text-left">
                </div>
              </div>
              <div class="q-field-bottom row no-wrap">
                <div class="q-field-helper col"></div>
              </div>
            </div>
          </div>
        </div>
        <q-field
          v-if="i.streetNumber === 'streetNumber' || exclude === false || inline === false"
          icon="home"
          label="Street Number"
          :label-width="2"
        >
          <q-input v-model="streetNumber.value" float-label="Your street number" />
        </q-field>
        <q-field
          v-if="i.postalCode === 'postalCode' || exclude === false || inline === false"
          icon="local post office"
          label="Postal Code"
          :label-width="2"
        >
          <q-input v-model="postalCode.value" float-label="Your postal code" />
        </q-field>
        <q-field
          v-if="i.city === 'city' || exclude === false || inline === false"
          icon="location city"
          label="City"
          :label-width="2"
        >
          <q-input v-model="city.value" float-label="Your city" />
        </q-field>
        <q-field
          v-if="i.state === 'state' || exclude === false || inline === false"
          icon="domain"
          label="State"
          :label-width="2"
        >
          <q-input v-model="state.value" float-label="Your state" />
        </q-field>
        <q-field
          v-if="i.country === 'country' || exclude === false || inline === false"
          icon=" "
          label="Country"
          :label-width="2"
        >
          <q-input v-model="country.value" float-label="Your Country" />
        </q-field>
      </div>
      <div>
        <p>{{ inputs }} {{ isInline }} </p>
      </div>
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
  name: 's-address',
  components: {
    QField,
    QInput,
    QBtn,
    QIcon
  },
  props: {
    lang: {
      type: String,
      default: 'br',
      required: false
    },
    inline: {
      type: Boolean,
      default: false,
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
    showHelpers: {
      type: Boolean,
      default: false,
      required: false
    }
  },
  data() {
    return {
      autocomplete: '',
      id: 'input',
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
          value: ''
      },
      streetNumber: {
          value: ''
      },
      postalCode: {
          value: ''
      },
      city: {
          value: ''
      },
      state: {
          value: ''
      },
      country: {
          value: ''
      },
      error: true,
      error2: false,
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

    let autocomplete = this.autocomplete;

    autocomplete = new google.maps.places.Autocomplete(
      document.getElementById(this.id),
      { types:['address'] }
    );

    autocomplete.setComponentRestrictions({'country': [this.lang]});

    autocomplete.addListener('place_changed', () => {
      const place = autocomplete.getPlace();
      const components = place.address_components;
      const type = place.types;

      if (type[0] === 'route'){
        let result = components.reduce((acc, cur, i) => {
          acc[i] = cur;

          return acc;
        }, {});

        this.route.value = result[0].long_name;
        this.city.value = result[2].long_name;
        this.state.value = result[3].long_name;
        this.country.value = result[4].long_name;
      }

      if (type[0] === 'street_address'){
        let result = components.reduce((acc, cur, i) => {
          acc[i] = cur;

          return acc;
        }, {});

        this.route.value = result[1].long_name;
        this.streetNumber.value = result[0].long_name;
        this.postalCode.value = result[6].long_name;
        this.city.value = result[3].long_name;
        this.state.value = result[4].long_name;
        this.country.value = result[5].long_name;
      }
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
    inputs() {
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
    },
    isInline() {
      console.log(this.inline)
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
