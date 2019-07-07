<template>
    <v-timeline-item
      :color="bubbleClassList"
      fill-dot
      :left="!isRight"
      :right="isRight"
    >
      <template v-slot:opposite>
        <span>
          {{ $t(`days.${event.title}`) }}
        </span>
      </template>
      <v-card>
        <v-card-title
          :class="event.color"
          class="lighten-1"
        >
          <h2 class="display-1 white--text font-weight-light">
            {{ $t(`days.${event.time}`) }}
          </h2>
        </v-card-title>
        <v-container>
          {{ $t(`days.${event.description}`) }}
        </v-container>
        <v-card-actions>
          <v-btn
            v-for="(action, index) in event.actions"
            :key="index"
            flat
            color="orange"
            :href="action.url"
          >
            {{ $t(`days.${action.label}`) }}
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-timeline-item>
</template>

<script>
export default {
  name: 'TimeItem',
  props: {
    event: {
      type: Object,
      requires: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  computed: {
    bubbleClassList() {
      return `${this.event.color} lighten-1`;
    },
    isRight() {
      return this.index % 2 === 0;
    }
  }
}
</script>
