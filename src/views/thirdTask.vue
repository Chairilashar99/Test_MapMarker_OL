<template>
    <div>
        <input type="text" v-model="coordinates" placeholder="Enter coordinates (latitude,longitude)">
        <button @click="addMarker">Add Marker</button>
        <div id="map" style="width: 100%; height: 400px;"></div>
        <p id="coordinatesDisplay">Current Coordinates: {{ coordinates }}</p>
    </div>
</template>

<script>
import 'ol/ol.css';
import { Map, View } from 'ol';
import TileLayer from 'ol/layer/Tile';
import OSM from 'ol/source/OSM';
import { fromLonLat } from 'ol/proj';
import Feature from 'ol/Feature';
import Point from 'ol/geom/Point';
import { Style, Icon } from 'ol/style';
import VectorSource from 'ol/source/Vector';
import VectorLayer from 'ol/layer/Vector';

export default {
    data() {
        return {
            map: null,
            coordinates: '',
        };
    },
    mounted() {
        this.initMap();
    },
    methods: {
        initMap() {
            const map = new Map({
                target: 'map',
                layers: [
                    new TileLayer({
                        source: new OSM(),
                    }),
                ],
                view: new View({
                    center: fromLonLat([110.3695, -7.7956]),
                    zoom: 10,
                }),
            });
            this.map = map;
        },
        addMarker() {
            const coordinates = this.coordinates.split(',');

            if (coordinates.length === 2) {
                const latitude = parseFloat(coordinates[0]);
                const longitude = parseFloat(coordinates[1]);

                if (!isNaN(latitude) && !isNaN(longitude)) {
                    const vectorSource = new VectorSource();
                    const feature = new Feature({
                        geometry: new Point(fromLonLat([longitude, latitude])),
                    });

                    const iconStyle = new Style({
                        image: new Icon({
                            anchor: [0.5, 1],
                            src: 'https://openlayers.org/en/latest/examples/data/icon.png',
                        }),
                    });

                    feature.setStyle(iconStyle);
                    vectorSource.addFeature(feature);

                    const vectorLayer = new VectorLayer({
                        source: vectorSource,
                    });

                    this.map.addLayer(vectorLayer);

                    this.map.getView().setCenter(fromLonLat([longitude, latitude]));


                    document.getElementById('coordinatesDisplay').textContent = `Current Coordinates: ${coordinates}`;
                } else {
                    alert('Invalid coordinates. Please enter valid latitude and longitude values.');
                }
            } else {
                alert('Invalid coordinates format. Please enter coordinates in the format "latitude,longitude".');
            }
        },
    },
};
</script>

<style scoped>
#map {
    width: 100%;
    height: 400px;
}
</style>