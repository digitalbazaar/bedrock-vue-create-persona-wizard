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
          color: {
            value: '#3498DB'
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
    async done(event) {
      const {waitUntil} = event;
      const p = sleep(2000);
      await waitUntil(p);
      console.log('Done!', this.form);
    }
  }
};

function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
</script>
<style>
</style>
