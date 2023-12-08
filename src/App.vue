<template>
  <div id="app">
    <Invoice />
  </div>
</template>

<script>
import Invoice from "./components/Invoice.vue";

export default {
  name: "App",
  components: {
    Invoice,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  background: #ddd;
  padding: 40px;
}

textarea {
  width: 100% !important;
  border: 1px solid #ddd !important;
}

.container {
  min-height: 29.7cm;
  margin: auto;
}

.invoice {
  background: #fff;
  width: 100%;
  padding: 50px;
}

.logo {
  width: 2.5cm;
}

.document-type {
  text-align: right;
  color: #444;
}

.conditions {
  font-size: 0.7em;
  color: #666;
}

.bottom-page {
  font-size: 0.7em;
}

table {
  font-size: 12px !important;
}

table td {
  padding: 0.45rem !important;
}

table td {
  font-size: 15px;
}

@media print {
  [data-invoicly="true"] {
    border: none !important;
  }

  .invoice {
    display: block;
  }

  .hide-elements {
    display: none;
  }

  @page {
    size: auto;
    /* auto is the initial value */
    margin: 30px 0;
    /* this affects the margin in the printer settings */
  }

  .container {
    width: 100% !important;
  }

  .invoice {
    font-size: 13px !important;
    color: black !important;
    padding: 0 !important;
  }

  .btn {
    display: none !important;
  }

  #logoForm {
    display: none;
  }

  table td {
    padding: 0.45rem !important;
  }

  .table > :not(caption) > * > * {
    color: black !important;
    font-size: 10px !important;
  }

  body {
    margin: 0;
    /* Remove default body margin */
    padding: 0;
    /* Remove default body padding */
  }

  textarea {
    resize: none;
  }
}

.editable {
  cursor: pointer;
}

.transparent-input {
  border: none;
  background: transparent;
  outline: none;
}

.text-right {
  text-align: right;
}

.flex-container {
  display: flex;
}

[data-invoicly="true"] {
  border: 1px dashed #ddd;
  padding: 5px;
}

.settings-div {
  /* display: none; */
  background-color: white;
  padding: 20px;
  border: 1px solid #ccc;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
</style>
