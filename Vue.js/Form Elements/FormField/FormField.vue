<template>
  <div class="field">
    <label v-if="label" class="label" :for="id">{{label}}</label>
    <input :type="type" class="input" :class="{'is-danger':this.$validator.errors.has(label)}" :tabindex="tabindex" :name="name" :id="id" :autocomplete="autocomplete" :value="value" @input="updateValue" @change="updateValue" @blur="$emit('blur')" :disabled="disabled" :required="required" :placeholder="placeholder" />
    <span v-show="this.$validator.errors.has(label)" class="subtitle is-6 has-text-danger">{{ this.$parent.errors.first(label) }}</span>
  </div>
</template>

<script>
export default {
    name: "FormField", //TODO: check if this can be with spaces
    //inject: ['$validator'],
    inject: {
        $validator: '$validator'
    },
    $_veeValidate: {
        name() {
            return this.label;
        },
        // fetch the current value from the innerValue defined in the component data.
        value() {
            return this.value;
        }
    },
    props: {
        value: String,
        placeholder:String,
        id: {
            type: String,
            default: () => {
                const rand = Math.floor((Math.random() * 10000) + 1); //TODO: Create enough margin so there won't be a chance it has the same ID as other elemnts. Change the method?
                const id = `undefined_${Date.now()*rand}`; //${this._uid}
                return id;
            }
        },
        label: {
            type: String,
            required: false
        },
        type: {
            type: String,
            default: "text"
        },
        name: {
            type: String,
            required: true
        },
        autocomplete: {
            type: String,
            required: false
        },
        disabled: {
            type: Boolean,
            default: false
        },
        required:{
            type:Boolean,
            default:false
        },
        tabindex:{
          type:Number
        },
        autocapitalize:{
          type:String,

        },
        autofocus:{
          type:Boolean
        }
    },
    computed: {

    },
    created: function() {
        console.log("Created");
    },
    mounted: function() {
        console.log("Mounted");
    },
    methods: {
        updateValue(e) {
            this.$emit("input", e.target.value);
        }
    }
};
</script>

<style scope>

</style>
