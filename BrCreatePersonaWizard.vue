<template>
  <div class="fit">
    <br-wizard
      :current-step-index="stepIndex"
      :total-steps="steps.length"
      @finish="done($event)"
      @index="stepIndex = $event">
      <br-wizard-step
        :heading="currentStep.heading"
        :image="currentStep.image"
        :icon="currentStep.icon"
        :subheading="currentStep.subheading">
        <div class="q-pb-xl full-width">
          <br-persona-name-form
            v-if="steps[stepIndex].name === 'Persona Name'"
            v-model="value.persona" />
          <br-persona-details-form
            v-if="steps[stepIndex].name === 'Persona Details'"
            v-model="value.persona" />
          <br-create-persona-review-card
            v-if="steps[stepIndex].name === 'Review and Submit'"
            :form="value" />
        </div>
      </br-wizard-step>
    </br-wizard>
  </div>
</template>

<script>
/*!
 * Copyright (c) 2019 Digital Bazaar, Inc. All rights reserved.
 */
'use strict';

import BrPersonaDetailsForm from './BrPersonaDetailsForm.vue';
import BrPersonaNameForm from './BrPersonaNameForm.vue';
import BrCreatePersonaReviewCard from './BrCreatePersonaReviewCard.vue';
import {BrWizard, BrWizardStep} from 'bedrock-vue-wizard';

export default {
  name: 'BrCreatePersonaWizard',
  components: {
    BrCreatePersonaReviewCard,
    BrPersonaNameForm,
    BrPersonaDetailsForm,
    BrWizard,
    BrWizardStep
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
      stepIndex: 0,
      steps: [
        {
          icon: {
            name: 'fas fa-walking',
            size: '65px',
            color: 'primary'
          },
          heading: 'Welcome, let\'s get started!',
          subheading: 'We need to walk through a few steps to create a' +
                  ' Persona.',
          name: 'Introduction',
        },
        {
          icon: {
            name: 'far fa-list-alt',
            size: '65px',
            color: 'primary'
          },
          heading: 'Let\'s name your Persona',
          name: 'Persona Name'
        },
        {
          icon: {
            name: 'far fa-list-alt',
            size: '65px',
            color: 'primary'
          },
          heading: 'Let\'s fill out some information about your Persona',
          name: 'Persona Details'
        },
        {
          icon: {
            name: 'fas fa-check-circle',
            size: '65px',
            color: 'primary'
          },
          heading: 'Does this look okay?',
          name: 'Review and Submit'
        }
      ]
    };
  },
  computed: {
    currentStep() {
      return this.steps[this.stepIndex];
    },
    form() {
      return this.value;
    },
  },
  methods: {
    done() {
      this.$emit('done');
    }
  }
};

</script>
<style>
</style>
