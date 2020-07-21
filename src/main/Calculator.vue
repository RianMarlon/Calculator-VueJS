<template>
    <div class="calculator">
        <Display :value="displayValue" />
        <Button label="AC" triple @onClick="clearMemory" />
        <Button label="/" operator @onClick="setOperator" />
        <Button label="7" @onClick="addDigit" />
        <Button label="8" @onClick="addDigit" />
        <Button label="9" @onClick="addDigit" />
        <Button label="*" operator @onClick="setOperator" />
        <Button label="4" @onClick="addDigit" />
        <Button label="5" @onClick="addDigit" />
        <Button label="6" @onClick="addDigit" />
        <Button label="-" operator @onClick="setOperator" />
        <Button label="1" @onClick="addDigit" />
        <Button label="2" @onClick="addDigit" />
        <Button label="3" @onClick="addDigit" />
        <Button label="+" operator @onClick="setOperator" />
        <Button label="0" double @onClick="addDigit" />
        <Button label="." @onClick="addDigit" />
        <Button label="=" operator @onClick="setOperator" />
    </div>
</template>

<script>
    import Display from '../components/Display';
    import Button from '../components/Button';

    export default {
        components: { Display, Button },
        data: function() {
            return {
                displayValue: '0',
                values: [0, 0],
                operator: null,
                index: 0,
                clearDisplay: false
            }
        },
        methods: {
            clearMemory() {
                Object.assign(this.$data, this.$options.data());
            },

            setOperator(operator) {
                if(this.index == 0) {
                    this.index = 1;
                    this.operator = operator;
                    this.clearDisplay = true;
                }

                else {
                    const equals = operator == '=';
                    const currentOperator = this.operator;
                    const values = this.values;

                    try {
                        this.values[0] = eval(`
                        ${values[0]} ${currentOperator} ${values[1]}
                        `);
                    }
                    catch(e) {
                        console.log(e);
                    }
                    this.values[1] = 0;

                    this.displayValue = this.values[0];
                    this.operator = (equals) ? null : operator;
                    this.clearDisplay = !equals;
                    this.index = (equals) ? 0 : 1;
                }
            },
            addDigit(n) {
                if(n == '.' && this.displayValue.includes('.')) {
                    return;
                }

                const clearDisplay = this.clearDisplay
                    || this.displayValue == '0' && n != '.';
                const currentValue = (clearDisplay) ? '' : this.displayValue;
                const newValue = currentValue + n;

                this.displayValue = newValue;
                this.clearDisplay = false;
                this.values[this.index] = newValue;
            }
        }
    }
</script>

<style>
    .calculator {
        width: 250px;
        display: grid;
        grid-template-columns: repeat(4, 25%);
        grid-template-rows: 90px repeat(5, 48px);
    }
</style>
