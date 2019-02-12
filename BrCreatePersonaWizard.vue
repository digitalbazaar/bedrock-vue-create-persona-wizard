<template>
  <q-stepper
    ref="stepper"
    v-model="currentStep"
    class="fit no-shadow"
    contractable>
    <q-step
      v-for="(step, index) in steps"
      :key="index"
      default
      :name="index"
      :title="step.title">
      <div class="column justify-center items-center">
        <q-icon
          size="100px"
          :name="step.iconName"
          class="text-primary q-my-lg" />
        <h3 class="text-weight-light q-my-sm">
          {{step.label}}
        </h3>
        <h6
          v-if="step.sublabel"
          class="text-weight-light q-my-md">
          {{step.sublabel}}
        </h6>
        <div
          v-show="index > 0"
          class="fit"
          style="max-width: 600px;">
          <div class="q-mx-xl q-mb-xl">
            <br-persona-name-form
              v-if="index === 1"
              v-model="value.persona" />
            <br-persona-details-form
              v-else-if="index === 2"
              v-model="value.persona" />
            <br-create-persona-review-card
              v-else
              :form="value" />
          </div>
        </div>
      </div>
    </q-step>
    <q-stepper-navigation class="absolute-bottom-right">
      <q-btn
        v-show="!firstStep"
        outline
        color="primary"
        size="md"
        label="Back"
        @click="previous()" />
      <q-btn
        v-if="!finalStep"
        class="q-ml-sm"
        color="primary"
        size="md"
        label="Next"
        @click="next()" />
      <q-btn
        v-else
        class="q-ml-sm"
        color="primary"
        size="md"
        label="Done"
        @click="done()" />
    </q-stepper-navigation>
  </q-stepper>
</template>

<script>
/*!
 * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
 */
'use strict';

import BrPersonaDetailsForm from './BrPersonaDetailsForm.vue';
import BrPersonaNameForm from './BrPersonaNameForm.vue';
import BrCreatePersonaReviewCard from './BrCreatePersonaReviewCard.vue';

export default {
  name: 'BrCreatePersonaWizard',
  components: {
    BrCreatePersonaReviewCard,
    BrPersonaNameForm,
    BrPersonaDetailsForm
  },
  props: {
    value: {
      type: Object,
      default: undefined,
      required: true
    }
  },
  data() {
    return {
      steps: [
        {
          iconName: 'fas fa-walking',
          label: 'Welcome, let\'s get started!',
          sublabel: 'We need to walk through a few steps to create a' +
                  ' Persona.',
          title: 'Introduction',
        },
        {
          iconName: 'far fa-list-alt',
          label: 'Let\'s name your Persona',
          title: 'Business Information'
        },
        {
          iconName: 'far fa-list-alt',
          label: 'Let\'s fill out some information about your Persona',
          title: 'Address Information'
        },
        {
          iconName: 'fas fa-check-circle',
          label: 'Does this look okay?',
          title: 'Review and Submit'
        }
      ],
      currentStep: 0
    };
  },
  computed: {
    form() {
      return this.value;
    },
    firstStep() {
      return this.currentStep === 0;
    },
    finalStep() {
      return this.currentStep === this.steps.length - 1;
    }
  },
  methods: {
    done() {
      this.$emit('done');
    },
    next() {
      this.$refs.stepper.next();
    },
    previous() {
      this.$refs.stepper.previous();
    }
  }
};

</script>
<style>
</style>
