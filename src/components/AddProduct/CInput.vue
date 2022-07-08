<template>
  <div class="input-form">

    <p class="label">
        {{ nameInput }}
        <span :class="{ 'd-none': !isRequired  }"></span>
    </p>

    <input 
        :type="type" 
        :placeholder="placeholder" 
        @input="$emit('input', $event.target.value)"
        :value="value"
        :class="{ 'invalid-input' : error }"
    >
    
    <p class="error-message" v-if="error">{{ error }}</p>
  </div>
</template>

<script>
export default {
    name: 'CInput',
    props: {
        type: {
            type: String,
            default: 'text'
        },
        error: {
            type: String,
            required: false
        },
        value: {
            type: String,
            required: true
        },
        nameInput: {
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

    .input-form {
        display: flex;
        flex-direction: column;
        width: 100%;
        margin-bottom: 16px;
        position: relative;
    }
    .label {
        position: relative;
        margin-bottom: 4px;
        width: fit-content;
        color: $dark-lesser;
        font-size: 10px;

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
    }
    
    input {
        padding: 9px 16px;
        border: 1px solid $white;
        background: $white;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        font-size: 12px;
        line-height: 15px;
        font-family: 'Source Sans Pro', sans-serif;

        &:focus {
            border: 1px solid $grey;
        }

        &::placeholder {
            font-family: 'Source Sans Pro', sans-serif;
            font-size: 12px !important;
            color: $grey;
        }

        &[type='number'] {
            -moz-appearance:textfield;
        }
        
        &::-webkit-outer-spin-button,
        &::-webkit-inner-spin-button {
            -webkit-appearance: none;
        }
    }
    
    .error-message{
        position: absolute;
        bottom: -14px;
        left: 0;
        color: $pink;
        font-size: 8px;
        line-height: 10px;
    }
</style>
