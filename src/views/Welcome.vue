<template>
  <div>
    <h1>{{ title }}</h1>
    <p v-if="isEnabled">{{ subtitle }}</p>
    <button @dblclick="toggle">切り替え</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      title: '初めてのVue.jsアプリです！',
      subtitle: 'ようこそ',
      isEnabled: true
    }
  },
  methods: {
    toggle() {
      this.isEnabled = !this.isEnabled
    }
  },
}
</script>
