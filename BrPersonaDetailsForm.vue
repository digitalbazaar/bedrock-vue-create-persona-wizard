<template>
  <div class="fit">
    <q-input
      v-model="givenName.value"
      :label="givenName.label"
      :error="$v.givenName.$error"
      @blur="$v.givenName.$touch"
      @keyup="$v.givenName.$touch" />
    <q-input
      v-model="familyName.value"
      :error="$v.familyName.$error"
      :label="familyName.label"
      @blur="$v.familyName.$touch"
      @keyup="$v.familyName.$touch" />
  </div>
</template>
<script>
/*!
  * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
  */
'use strict';

import {minLength, required} from 'vuelidate/lib/validators';

export default {
  name: 'BrPersonaDetailsForm',
  props: {
    value: {
      type: Object,
      default: () => ({})
    }
  },
  validations: {
    familyName: {
      value: {
        minLength: minLength(1),
        required
      }
    },
    givenName: {
      value: {
        minLength: minLength(1),
        required
      }
    }
  },
  computed: {
    familyName() {
      return this.value.familyName;
    },
    givenName() {
      return this.value.givenName;
    },
    valid() {
      return !this.$v.$invalid;
    }
  },
  created() {
    const updatedLabels = _applyDefaultLabels({
      data: this.value,
      labels: {
        familyName: 'Last Name',
        givenName: 'First Name'
      }
    });
    this.$emit('input', updatedLabels);
  }
};
// TODO: Move to bedrock-web-forms
function isString(str) {
  return str && typeof str === 'string';
}

function _applyDefaultLabels({data, labels}) {
  return Object.keys(data).reduce((acc, key) => {
    acc[key] = isString(data[key].label) ? data[key] :
      {
        ...data[key],
        label: labels[key]
      };
    return acc;
  }, {});
}
</script>
<style>
</style>
