<template>
  <div>
    <v-tabs
      v-model="active"
      color="cyan"
      dark
      slider-color="yellow"
    >
      <v-tab ripped>
        Example
      </v-tab>
      <v-tab-item>
      </v-tab-item>
    </v-tabs>

    <div class="text-xs-center mt-3">
      <v-btn @click="next">{{ buttonText }}</v-btn>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Index',
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
      switch(this.active) {
        case 0: return 'Zum Samstag'
        case 1: return 'Zum Sonntag'
        default: return 'Zum Freitag'
      }
    }
  }
}
</script>
