<template>
    <div>
        <label>{{ customLabel }}</label>
        <!-- <input 
            type="range"
            :value="value"
            v-bind="$attrs"
            :class="inputClasses"
            @input="$emit('input', $event.target.value)"> -->
        <input 
            type="range"
            :value="valor"
            v-bind="$attrs"
            :class="inputClasses"
            @input="atualizar">
    </div>
</template>

<script>
export default {
    // não deixa os elementos que estão sendo setados no componente ocupar o root ( DIV ) no caso mas sim input
    inheritAttrs: false,
    model: {
        prop: 'valor'
    },
    props: {
        label: String,
        valor: [Number, String],
        inputClasses: [String, Object, Array]
    },
    data () {
        return {
            valorAtual: this.valor || this.$$attrs.min
        }
    },
    computed: {
        customLabel() {
            return `${this.label} (R$ ${this.valorAtual})`
        }
    },
    methods: {
        atualizar(event) {
            const valor = event.target.value;
            this.$emit('input', valor);
            this.valorAtual = valor;
        }
    }
}
</script>
