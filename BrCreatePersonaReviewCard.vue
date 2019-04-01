<template>
  <div class="fit">
    <q-card>
      <q-card-section>
        <div class="text-h5">
          Summary
        </div>
      </q-card-section>
      <q-separator />
      <q-card-section>
        <div>
          <div class="q-title text-weight-light q-my-md">
            Persona Information
          </div>
        </div>
        <div
          v-for="data in form.persona"
          :key="data.label">
          <div class="text-uppercase text-bold q-mt-md q-mb-xs">
            {{data.label}}
          </div>
          <div>
            {{data.value}}
          </div>
        </div>
      </q-card-section>
    </q-card>
  </div>
</template>
<script>
/*!
 * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
 */
'use strict';

export default {
  name: 'BrCreatePersonaReviewCard',
  props: {
    form: {
      type: Object,
      default: undefined,
      required: true
    }
  }
};
</script>
<style>
</style>
