<template>
  <div class="fit">
    <q-input
      v-model="name.value"
      :label="name.label"
      :error="$v.name.$error"
      hint="Example: Business, Education, Gaming, etc."
      @blur="$v.name.$touch"
      @keyup="$v.name.$touch" />
  </div>
</template>
<script>
/*!
  * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
  */
'use strict';

import {minLength, required} from 'vuelidate/lib/validators';

export default {
  name: 'BrPersonaNameForm',
  props: {
    value: {
      type: Object,
      default: () => ({})
    }
  },
  validations: {
    name: {
      value: {
        minLength: minLength(1),
        required
      }
    }
  },
  computed: {
    name() {
      return this.value.name;
    },
    valid() {
      return !this.$v.$invalid;
    }
  },
  created() {
    const updatedLabels = _applyDefaultLabels({
      data: this.value,
      labels: {
        name: 'Profile Name',
        color: 'Profile Color'
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
