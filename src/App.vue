<template>
  <!--ارسال 2 دیتا به کامپوننت-->
  <div class="flex flex-row justify-between">
    <Option
      :arrays="continents"
      keyName="id"
      titleName="name"
      :place="places[0]"
      @send:data="getCountry"
    ></Option>
    <Option
      :arrays="keshvarha"
      keyName="id"
      titleName="name"
      :place="places[1]"
      @send:data="getCity"
    ></Option>

    <Option
      :arrays="shahra"
      keyName="id"
      titleName="name"
      :place="places[2]"
    ></Option>
  </div>
</template>

<script setup>
import { ref, watch, reactive } from "vue";
import Option from "./components/Option.vue";

let places = ["قاره", "کشور", "شهر"];
let continents = reactive([
  { id: 1, name: "Asia" },
  { id: 2, name: "NorthAmerica" },
  { id: 3, name: "Europe" },
]);

let continentIds = [];
let continentNames = [];
for (let i = 0; i < continents.length; i++) {
  continentIds.push(continents[i].id);
  continentNames.push(continents[i].name);
}

let countries = reactive([
  { id: 1, name: "Iran", continent_id: 1 },
  { id: 2, name: "Canada", continent_id: 2 },
  { id: 3, name: "USA", continent_id: 2 },
  { id: 4, name: "Germany", continent_id: 3 },
  { id: 5, name: "France", continent_id: 3 },
  { id: 6, name: "Malaysia", continent_id: 1 },
]);
let cities = reactive([
  { id: 1, name: "Tehran", c_id: 1 },
  { id: 2, name: "Vancouver", c_id: 2 },
  { id: 3, name: "Newyork", c_id: 3 },
  { id: 4, name: "Mashhad", c_id: 1 },
  { id: 5, name: "Tabriz", c_id: 1 },
  { id: 6, name: "Toronto", c_id: 2 },
  { id: 7, name: "Montreal", c_id: 2 },
  { id: 8, name: "Hamburg", c_id: 4 },
  { id: 9, name: "Berlin", c_id: 4 },
  { id: 10, name: "Munich", c_id: 4 },
  { id: 11, name: "Paris", c_id: 5 },
  { id: 12, name: "Lyon", c_id: 5 },
  { id: 13, name: "LosAngeles", c_id: 3 },
  { id: 14, name: "Chicago", c_id: 3 },
  { id: 15, name: "KualaLumpur", c_id: 6 },
]);
const keshvarha = reactive([]);
const shahra = reactive([]);

const ContinentId = ref("");
const CountryId = ref("");

function getCountry(parameter) {
  ContinentId.value = parameter;
}

function getCity(parameter) {
  CountryId.value = parameter;
}

//دریافت لیست کشورها
//باید خودش و زیر مجموعش موقع تغییر ریست بشن
watch(ContinentId, (newValue, oldValue) => {
  keshvarha.splice(0, keshvarha.length);
  shahra.splice(0, shahra.length);
  for (let i = 0; i < countries.length; i++) {
    if (countries[i].continent_id == newValue) {
      keshvarha.push(countries[i]);
    }
  }
});

//دریافت لیست شهرها
watch(CountryId, (newValue, oldValue) => {
  shahra.splice(0, shahra.length);
  for (var i = 0; i < cities.length; i++) {
    if (newValue == cities[i].c_id) {
      shahra.push(cities[i]);
    }
  }
});

function showId(selectContinent, selectCountry, selectCity) {
  console.log("ایدی قاره :  ", selectContinent);
  console.log("ایدی کشور :  ", selectCountry);
  console.log("ایدی شهر  :  ", selectCity);
}
</script>
