<template>
  <img src="" alt="" />
  <h1>{{ name }}</h1>
  <table>
    <thead></thead>
    <tbody>
      <tr class="d-flex flex-column">
        <td class="fw-bold">Capital:</td>
        <td>{{ capital }}</td>
      </tr>
      <tr class="d-flex flex-column">
        <td class="fw-bold">Area:</td>
        <td>{{ area }}</td>
      </tr>
      <tr class="d-flex flex-column">
        <td class="fw-bold">Borders:</td>
        <td>
          <ul>
            <li v-for="(border, index) in borders" :key="index">
              {{ border }}
            </li>
          </ul>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      capital: "",
      alphacode: "",
      area: "",
      borders: [],
    };
  },
  methods: {
    async getCountryByAlphaCode() {
      this.alphacode = this.$route.params.alpha3Code;
      const response = await fetch(
        `https://ih-countries-api.herokuapp.com/countries/${this.alphacode}`
      );
      const finalResponse = await response.json();
      console.log(finalResponse);
      this.name = finalResponse.name.common;
      this.capital = finalResponse.capital[0];
      this.area = finalResponse.area;
      this.borders = finalResponse.borders;
    },
  },
  mounted() {
    this.getCountryByAlphaCode();
  },
  computed: {
    countryCode() {
      return this.$route.params.alpha3Code;
    },
  },
  watch: {
    countryCode(newCountryCode) {
		this.getCountryByAlphaCode();
	},
  },
};
</script>

<style></style>
