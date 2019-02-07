<template>
  <q-page
    class="column gutter-md background"
    padding>
    <div class="column items-center">
      <br-create-persona-wizard />
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
    return {};
  }
};
</script>
<style>
</style>
