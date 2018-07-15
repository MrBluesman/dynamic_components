
<template>
    <div>
        <input ref="autocomplete"
               placeholder="Search"
               class="search-location"
               onfocus="value = ''"
               type="text" />
    </div>

</template>

<script>
    export default {
        name: "Location",
        data () {
          return {
              place: {
              }
          }
        },
        mounted() {
            this.autocomplete = new google.maps.places.Autocomplete(
                (this.$refs.autocomplete),
                {types: ['geocode']}
            );

            this.autocomplete.addListener('place_changed', () => {
                this.place = this.autocomplete.getPlace();
                this.place.ac = this.place.address_components;
                let lat = this.place.geometry.location.lat();
                let lon = this.place.geometry.location.lng();
                let city =  this.place.ac[0]["short_name"];
            });
        }
    }
</script>

<style scoped>

</style>