<template>
  <div class="input-form">

    <p class="label">
        {{ nameInput }}
        <span :class="{ 'd-none': !isRequired  }"></span>
    </p>

    <input 
        :placeholder="placeholder" 
        v-model="modelNumber"
        :type="indicatorChange ? 'number' : 'text'"
        @focus="indicatorChange = true"
        @blur="indicatorChange = false"
        :class="{ 'invalid-input' : error }"
    >

    <p class="error-message" v-if="error">{{ error }}</p>
  </div>
</template>

<script>

export default {
    name: 'InputNumber',
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
            type: Number,
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
        }
        },
    data() {
        return {
            realNumber: '',
            indicatorChange: false, 
        }
    },
    computed: {
        modelNumber: {
            get() {
                return this.indicatorChange ? this.realNumber : this.realNumber.toLocaleString()
            },
            set(value) {
                this.realNumber = +value.replace(/\s/g, "")
                this.$emit('input', this.realNumber)
            },
        },
    },
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
    input {
        padding: 9px 16px;
        border: 1px solid $white;
        background: $white;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        font-size: 12px;
        line-height: 15px;

        &:focus {
            border: 1px solid $white;
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
