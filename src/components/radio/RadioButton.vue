<template>
    <p class="control">
        <button
            class="radio button"
            :class="[isChecked ? type : '', size, { 'is-disabled': disabled }]"
            @click="changed">
            <slot></slot>
            <input
                type="radio"
                :disabled="disabled"
                :checked="isChecked"
                :name="name"
                :value="this.value">
        </button>
    </p>
</template>

<script>
    export default {
        name: 'bRadioButton',
        props: {
            value: [String, Number, Boolean],
            type: {
                type: String,
                default: 'is-primary'
            },
            disabled: Boolean,
            name: String
        },
        data() {
            return {
                // Used internally by Radio Group
                size: '',
                isChecked: false,
                isRadioButton: true
            }
        },
        methods: {
            changed(event) {
                this.$parent.updateValue(this.value, event)
            }
        },
        created() {
            if (!this.$parent.isRadioGroupComponent) {
                this.$destroy()
                throw new Error('You should wrap Radio Button on a Radio Group')
            }
        }
    }
</script>
