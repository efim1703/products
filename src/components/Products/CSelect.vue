<template>
    <div class="select">
        <p 
            :class="[{ 'border-radius-bottom-none' : showOptions }, 'title']" 
            @click="clickSelect()"
        >
            <span >{{ optionIsActive.name }}  </span>
            <svg width="8" height="6" viewBox="0 0 8 6" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M7.48532 1.24264L4.24268 4.48528L1.00003 1.24264" stroke="#B4B4B4"/></svg>
        </p>

        <div class="options" v-if="showOptions">
            <p
                v-for="option in options"
                :key="option.value"
                @click="clickOption(option)"
            >
                {{ option.name }}
            </p>
        </div>
    </div>
</template>

<script>
export default {
  name: 'CSelect',
  props: {
    options: {
        type: Array,
        required: true
    },
    optionIsActive: {
        type: Object,
        required: true
    }
  },
  data() {
    return {
        showOptions: false,
    }
  },
  methods: {
    clickSelect() {
        this.showOptions = !this.showOptions
    },
    clickOption(option) {
        this.$emit('option-change',option.value);
        this.showOptions = false
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';

    .select {
        position: relative;
        max-width: 124px;
        color: $grey;
        font-size: 12px;
        cursor: pointer;
    }
    .title {
        display: flex;
        align-items: center;
        padding: 10px 16px;
        background: $white;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;

        svg {
            margin-left: 6px;
        }
    }
    .options {
        position: absolute;
        top: 36px;
        right: 0;
        left: 0;
        text-align: center;
        background: $white;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 0px 0px 4px 4px;
        z-index: 999;

        p {
            padding: 6px 0px;
        }
    }
</style>
