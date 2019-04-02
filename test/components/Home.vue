<template>
  <q-page
    class="column q-col-gutter-md background"
    padding>
    <div class="column items-center">
        <br-create-persona-wizard
          v-model="form"
          @done="done" />
    </div>
  </q-page>
</template>
<script>
/*!
 * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
 */
'use strict';

import {BrCreatePersonaWizard} from 'bedrock-vue-create-persona-wizard';

export default {
  name: 'Home',
  components: {BrCreatePersonaWizard},
  data() {
    return {
      form: {
        persona: {
          name: {
            value: ''
          },
          familyName: {
            value: ''
          },
          givenName: {
            value: ''
          }
        }
      }
    };
  },
  methods: {
    done() {
      console.log('Done!', this.form);
    }
  }
};
</script>
<style>
</style>
