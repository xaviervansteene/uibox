<template>
  <button :disabled="noClick" @click="emitClick()" :class="[{'shaky': isError}, 'c_button c_button-primary']">
    <div v-show="loading" class="spinner-border spinner-border-sm" role="status">
      <span class="sr-only">Chargement...</span>
    </div>
    <i v-if="icon" :class="icon"></i>
    <span v-show="!loading">{{ label }}</span>
  </button>
</template>

<script>
export default {
  name: 'Btn',
  props: {
    label: {
      type: String,
      required: true
    },
    icon: {
      type: String,
      required: false
    },
    state: {
      type: Boolean,
      required: false,
      default: false
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false
    },
    spinner: {
      type: Boolean,
      required: false,
      default: true
    },
    error: {
      type: Boolean,
      required: false,
      default: false
    }
  },
  data () {
    return {
      noClick: this.disabled,
      loading: this.state,
      isError: this.error
    }
  },
  methods: {
    emitClick () {
      // this.noClick = true
      this.isError = false
      this.loading = !!this.spinner
      this.$emit('action', this)
    }
  },
  watch: {
    disabled () {
      this.noClick = this.disabled
    },
    isError () {
      const self = this
      setTimeout(function () { self.isError = false }, 500)
    }
  }
}
</script>

<style lang="scss">
.shaky {
  position: relative;
  animation: shake 0.05s linear;
  animation-iteration-count: 5;
}

.c_button{
  i{
    font-size:24px;
    margin-right:15px;
  }

  &.secondary{
    background:#fff!important;
    color:rgb(75,137,251)!important;
  }

}

@keyframes shake {
  0% {
    margin-left: 3px;
  }
  50% {
    margin-left: -3px;
  }
  100% {
    margin-left: 0;
  }
}
</style>
