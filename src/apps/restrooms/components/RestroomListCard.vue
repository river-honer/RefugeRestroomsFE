<template>
    <v-card
      flat
      outlined
      class="mb-10"
      @mouseover="hover = true"
      @mouseleave="hover = false"
    >
      <v-row>
        <v-col cols="9">
          <v-card-title
            class="mt-n4"
          >{{ restroom.name }}</v-card-title>
          <v-card-text>
            {{ restroom.street }}, {{ restroom.city }}, {{ restroom.state }}
          </v-card-text>
          <v-row>
            <v-chip
              class="ml-6"
              color="primary"
              :disabled="!restroom.unisex"
            >
              Unisex
            </v-chip>
            <v-chip
              class="ml-2"
              color="primary"
              :disabled="!restroom.accessible"
            >
              Accessible
            </v-chip>
            <v-chip
              class="ml-2"
              color="primary"
              :disabled="!restroom.changingTable"
            >
              Changing Table
            </v-chip>
          </v-row>
        </v-col>
        <v-col
          cols="3"
          align-self="center"
        >
          <span class="display-2">{{ restroom.distance }}</span>
          <span class="title">KM</span>
        </v-col>
      </v-row>
    </v-card>
</template>

<script lang="ts">
import Restroom from '../models/restroom';

export default {
  name: 'restroom-list-card',
  props: {
    restroom: {
      type: Restroom,
      required: true,
    },
  },
  data() {
    return {
      hover: false,
    };
  },
  watch: {
    hover(value) {
      if (value === true) {
        this.$emit('hover', {
          latLng: [this.restroom.latitude, this.restroom.longitude],
        });
      }
    },
  },
};
</script>
