<template>
    <div class="address">
        Address:  {{data.Address}}
    </div>
    <div class="carparkno">
        Car Park No:  {{data.Car_park_no}}
    </div>
    <div class="lots">
        Current Lots Available: {{data.Current_Lots_Available}}
    </div>
    <div class="distance">
        Distance:  {{data.Distance}}
    </div>
    <div class="map" :id="`map-${index}`"></div>
</template>

<script>
import { Loader } from "@googlemaps/js-api-loader";
const loader = new Loader({
  //apiKey: import.meta.env.VITE_APIKEY,
  apiKey: window.atob("QUl6YVN5RFY1SlNRMkM1ZF84RV83bkxGY3hNU3FjbmdoLTI3bjZz"),
  version: "weekly",
});

export default {
    data() {
        return {
            center: { lat: Number(this.data.Latitude), lng: Number(this.data.Longitude) }
        };
    },
    props: ['data', 'index'],
    methods: {
        genMap(){
            loader.load().then(() => {
                const map = new google.maps.Map(document.getElementById(`map-${this.index}`), {
                    center: this.center,
                    zoom: 16,
                });
                const myLatLng = this.center;
                new google.maps.Marker({
                    position: myLatLng,
                    map,
                    title: "Let's go!",
                });
            });
        }
    },
    mounted() {
        this.genMap();
    },
    updated() {
        this.genMap();
    }
}
</script>

<style>
    .map {
        height: 600px;
    }
    .address {
    color: #21bea0;
    background-color: #f4f9f7;
    height: 60px;
    padding-left: 20px;
    }
    .carparkno {
    color: #21bea0;
    background-color: #f4f9f7;
    height: 60px;
    padding-left: 20px;
    }
    .lots {
    color: #21bea0;
    background-color: #f4f9f7;
    height: 60px;
    padding-left: 20px;
    }
    .distance {
    color: #21bea0;
    background-color: #f4f9f7;
    height: 60px;
    padding-left: 20px;
    }
</style>