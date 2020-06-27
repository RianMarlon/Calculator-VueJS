<template>
    <button class="button" 
        :class="{ double, triple, operator }"
        @click="$emit('onClick', label)">
        {{ label }}
    </button>
  
</template>

<script>
    export default {
        props: {
            label: {},
            double: { type: Boolean },
            triple: { type: Boolean },
            operator: { type: Boolean }
        }
    }
</script>

<style>

    :root {
        --bg-button: #F0F0F0;
        --border-button: solid 1px #888;
    }
    
    .button {
        grid-column: span 1;
        font-size: 1.5em;
        color: #444;
        background-color: var(--bg-button);
        border: none;
        border-right: var(--border-button);
        border-bottom: var(--border-button);
        outline: none;
    }

    .button.double {
        grid-column: span 2;
    }

    .button.triple {
        grid-column: span 3;
    }

    .button.operator {
        grid-column: span 1;
        background-color: #FA8231;
        color: #FFF;
    }

    .button:active {
        background-color: #CCC;
    }

    .button.operator:active {
        background-color: #FA8231CC;
    }

</style>