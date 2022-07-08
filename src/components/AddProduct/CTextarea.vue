<template>
  <div class="textarea-form">

    <p>
        {{ nameTextarea }}
        <span :class="{ 'd-none': !isRequired  }"></span>
    </p>

    <textarea 
        type="text" 
        :placeholder="placeholder"
        @input="$emit('input', $event.target.value)"
        :value="value"
    />

  </div>
</template>

<script>

export default {
  name: 'CTextarea',
  props: {
    value: {
        type: String,
        required: true
    },
    nameTextarea: {
        type: String,
        required: true
    },
    placeholder: {
        type: String,
        default: ''
    },
    isRequired: {
        type: Boolean,
        default: false
    },
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';

    .textarea-form {
        display: flex;
        flex-direction: column;
        width: 100%;
        margin-bottom: 16px;
    }
    p {
        position: relative;
        margin-bottom: 4px;
        width: fit-content;
        color: $dark-lesser;
        font-size: 10px;
    }
    span {
        position: absolute;
        top: 0;
        right: -4px;
        width: 4px;
        height: 4px;
        display: block;
        background-color: $pink;
        border-radius: 50%;
    }
    textarea {
        min-height: 88px;
        padding: 9px 16px;
        border: 1px solid $white;
        resize: none;
        background: $white;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        font-family: 'Source Sans Pro', sans-serif;
        font-size: 12px;
        line-height: 15px;

        &:focus {
            border: 1px solid $grey;
        }

        &::placeholder {
            font-family: 'Source Sans Pro', sans-serif;
            font-size: 12px !important;
            color: $grey;
        }
    }
</style>
