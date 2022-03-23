<template>
  <div id="app">
    <img v-bind:src="dndLogo">
    <h1>List of Dungeons and Dragons Weapons and Classes</h1>
    <p>Data source: <a href="https://api.open5e.com/"><code>https://api.open5e.com/</code></a></p>
    <w-types />
    <p-classes />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import WTypes from './components/WeaponList.vue';
import PClasses from './components/PlayerClasses.vue';


@Component({
  components: {
    WTypes,
    PClasses,
  },
})
export default class App extends Vue {
  private readonly dndLogo = "https://ph-test-11.slatic.net/p/b72fa413bc209775f3444f9d3900df12.png"
}
</script>

<style>
body{
  background-color: lightgoldenrodyellow;
}

img {
  height: 200px;
  width: 200px;
}

table {
  border: 4px solid black;
  margin: 1em;
}

#WeaponsTable {
background-color: hsl(28, 29%, 61%);
}

#ClassTable{
  background-color: seagreen;
}

#WeaponsTable tr:nth-child(odd) {
  background-color: burlywood;
}

#WeaponsTable tr:first-child {
  background-color: hsl(28, 29%, 61%);
}

#ClassTable tr:nth-child(odd) {
  background-color: lightseagreen;
}

#ClassTable tr:first-child {
  background-color: seagreen;
}

table tr:nth-child(even) {
  background-color: white;
}

code {
  font-size: 125%;
}

table td:nth-child(2) {
  font-style: italic;
}

code:hover {
  font-style: italic;
}

h2 + select {
  background-color: hsl(28, 29%, 61%);
  font-weight: bold;
}

#ClassSelect{
  background-color: seagreen;
  font-weight: bold;
}

h1 {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}

#sword{
  height: 50px;
  width: 50px;
  padding-right: 0.5em;
}

#spell {
  height: 50px;
  width: 50px;
  padding-right: 0.5em;
}
</style>