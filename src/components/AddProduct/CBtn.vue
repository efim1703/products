<template>
  <button :disabled="isDisabled" @click="$emit('click', $event)">
    <slot/>
  </button>
</template>

<script>

export default {
  name: 'CBtn',
  props: {
    isDisabled: {
        type: Boolean,
        default: false
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';

  button {
      width: 100%;
      padding: 10px;
      margin-top: 8px;
      background: #7BAE73;
      color: #fff;
      font-family: 'Inter', sans-serif;
      font-weight: 600;
      font-size: 12px;
      border-radius: 10px;
      transition: ease .4s;

      &:hover {
        background: #94cc8b;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      }
      
      &:disabled {
          background: #EEEEEE;
          color: $grey;
      }
  }
</style>