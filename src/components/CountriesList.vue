<template>
  <h1>Country List</h1>
  <h1 v-for="(country, index) in countries" :key="index"> 
    {{country.name.common}}
    </h1>
</template>

<script>
export default {
  name: "CountriesList",
  data() {
    return {
      //definimos un valor de datos estilo array para recibir la info del api
      countries: null,
    };
  },
  methods: {
    async fetchCountries() {
      const response = await fetch(
        "https://ih-countries-api.herokuapp.com/countries"
      );
      const finalResponse = await response.json();
      // console.log(finalResponse);//VERIFICAMOS MEDIANTES UNA LLAMADA A CONSOLA QUE RECIBIMOS LOS DATOS
      this.countries = finalResponse;
    },
  },
  //usamos el created hook para hacer nuestra llamada inicial a nuestra base de datos.
  //no usamos async en este caso porque la asincronia la maneja la funcion fetchCountries. El hook created() solo se encarga de llamar la funcion fetchCountries
  created() {
    this.fetchCountries();
  },
};
</script>

<style></style>
