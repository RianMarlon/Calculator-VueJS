<template>
  <div id="app">
      <h1>Calculator</h1>
      <Calculator />
  </div>
</template>

<script>
    import Calculator from './main/Calculator';

    export default {
        components: { Calculator }
    }
</script>

<style>

    * {
        box-sizing: border-box;
        font-family: "Roboto Mono", monospace;
    }

    body {
        margin: 0;
    }

    #app {
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;

        text-align: center;
        color: #FFF;
        background: linear-gradient(to right, rgb(83, 105, 118), rgb(41, 46, 73));
    }

</style>
