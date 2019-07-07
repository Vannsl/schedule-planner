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
            <v-img
              v-if="day.img"
              aspect-ratio="2"
              :src="day.img"
            ></v-img>
            <v-timeline :dense="dense">
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
      <v-btn @click="next">
        {{ $t('home.goto', { day: days[nextIndex].name }) }}
      </v-btn>
    </div>
  </div>
</template>

<script>
import data from '@/data'
import TimeItem from '@/components/TimeItem'

export default {
  name: 'Index',
  components: {
    'time-item': TimeItem
  },
  data () {
    return {
      active: 0,
      isHydrated: false
    }
  },
  methods: {
    next() {
      window.scrollTo(0, 0)
      this.$nextTick(() => {
        this.active = this.nextIndex;
      })
    }
  },
  computed: {
    nextIndex() {
      return (this.active + 1) % this.days.length;
    },
    days() {
      const { days } = data;
      return days;
    },
    slugs() {
      return this.days.map(day => (day.name));
    },
    dense() {
      return this.isHydrated
        ? this.$vuetify.breakpoint.xsOnly
        : true
    }
  },
  mounted() {
    this.isHydrated = true;
  }
}
</script>
