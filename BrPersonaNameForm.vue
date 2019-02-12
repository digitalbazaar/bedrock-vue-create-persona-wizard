<template>
  <div class="fit">
    <q-field
      class="col-5 q-pr-md"
      :error="$v.name.$error"
      helper="Example: Business, Education, Gaming, etc."
      orientation="vertical">
      <q-input
        v-model="name.value"
        :float-label="name.label"
        placeholder="Please type a name for your Persona..."
        @blur="$v.name.$touch"
        @keyup="$v.name.$touch" />
    </q-field>
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
        name: 'Persona Name'
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
