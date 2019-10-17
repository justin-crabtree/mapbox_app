<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div id="map"></div>
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 0;
}
#map {
  top: 0;
  bottom: 0;
  height: 700px;
}
</style>

<script>
export default {
  data: function() {
    return {
      message: "Venice, FL!",
      places: [
        {
          longitude: -82.39323,
          latitude: 27.150783,
          description: "Home"
        },
        {
          longitude: -82.446086,
          latitude: 27.099614,
          description: "Upper Crust Cafe and Bakery"
        },
        {
          longitude: -82.460151,
          latitude: 27.099909,
          description: "Venice Beach"
        }
      ]
    };
  },
  created: function() {},
  mounted: function() {
    mapboxgl.accessToken = "pk.eyJ1IjoiZHphZ2hpYW4iLCJhIjoiY2pzbnF0NmV0MGY2czQzbXBpMjcwMzRmNiJ9.Jei4-17Vu7hJSerisjPCEg";
    var map = new mapboxgl.Map({
      container: "map", // container id
      style: "mapbox://styles/mapbox/streets-v11", // stylesheet location
      center: [-82.4542633, 27.0997775], // starting position [lng, lat]
      zoom: 12 // starting zoom
    });

    this.places.forEach(function(place) {
      var popup = new mapboxgl.Popup({ offset: 25 }).setText(place.description);
      new mapboxgl.Marker()
        .setLngLat([place.longitude, place.latitude])
        .setPopup(popup) // sets a popup on this marker
        .addTo(map);
    });
  },
  methods: {}
};
</script>
