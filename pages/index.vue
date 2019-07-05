<template>
  <div>
    <v-tabs
      v-model="active"
      color="cyan"
      dark
      slider-color="yellow"
    >
      <v-tab
        v-for="slug in slugs"
        :key="slug"
        ripped
      >
        {{ $t(`days.${slug}`) }}
      </v-tab>
      <v-tab-item
        v-for="day in days"
        :key="day.name"
      >
        <v-layout
          column
          justify-center
          align-center
        >
          <v-flex
            xs12
            sm8
            md6
          >
            <item-image />
            <v-timeline :dense="$vuetify.breakpoint.xsOnly">
              <time-item
                v-for="(event, index) in day.events"
                :key="index"
                :event="event"
                :index="index"
              />
            </v-timeline>
          </v-flex>
        </v-layout>
      </v-tab-item>
    </v-tabs>

    <div class="text-xs-center mt-3">
      <v-btn @click="next">{{ buttonText }}</v-btn>
    </div>
  </div>
</template>

<script>
import data from '@/data'
import TimeItem from '@/components/TimeItem'
import ItemImage from '@/components/ItemImage'

export default {
  name: 'Index',
  components: {
    'time-item': TimeItem,
    'item-image': ItemImage
  },
  data () {
    return {
      active: null,
    }
  },
  methods: {
    next() {
      const active = parseInt(this.active)
      this.active = (active < 2 ? active + 1 : 0)
      window.scrollTo(0, 0)
    }
  },
  computed: {
    buttonText() {
      const index = this.active + 1 < this.days.length ? this.active + 1 : 0;
      return `Go to ${this.days[index].name}`;
    },
    days() {
      const { days } = data;
      return days;
    },
    slugs() {
      return this.days.map(day => (day.name));
    }
  }
}
</script>
