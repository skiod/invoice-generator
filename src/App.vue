<template>
  <div id="app">
    <div class="hide-elements center-navbar">
    <nav class="navbar navbar-expand-lg navbar-dark fixed-top p-2">
      <a class="navbar-brand" href="#">Invoice Generator</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="fa fa-bars"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ml-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Services</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Contact</a>
          </li>
        </ul>
      </div>
    </nav>
</div>

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
@import "./assets/style.css";
</style>
