<template>
  <div>
    <div
      class="map"
      ref="map"
    ></div>
    <template v-if="Boolean(this.google) && Boolean(this.map)">
      <slot
        :google="google"
        :map="map"
      />
    </template>
  </div>
</template>
 
<script>
 
  import GoogleMapsApiLoader from "google-maps-api-loader";
 
  export default {
    props: {
      configMap: Object,
      apiKey: String
    },
 
    data() {
      return {
        google: null,
        map: null
      };
    },
 
    async mounted() {
      const googleMapApi = await GoogleMapsApiLoader({
        apiKey: this.apiKey
      });
      this.google = googleMapApi;
      this.initializeMap();
    },
 
    methods: {
      initializeMap() {
        const mapContainer = this.$refs.map;
        this.map = new this.google.maps.Map(mapContainer, this.configMap);
      }
    }
 
  };
</script>
 
<style scoped>
  .map {
    max-width: 1920px;
    min-height: 100%;

  }
</style>