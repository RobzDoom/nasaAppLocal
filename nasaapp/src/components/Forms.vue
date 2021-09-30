<template>
    <div>
        Choose Camera
        <div class="FormDate">
            <input type="number" placeholder="Year" v-model="year">
            <span>/</span>
            <input type="number" placeholder="Month" v-model="month">
            <span>/</span>
            <input type="number" placeholder="Day" v-model="day">
        </div>
        <button @click="getRoversByDateAndCamera">Check Date Button</button>

        <div v-if="noImages" class="noImages"> There are no images available for chosen date. Choose a different date.
        </div>
        <div v-if="yesImages" class="yesImages"> There are a total of {{this.imageCount}} Images for this date </div>

        <div v-if="yesImages">
            <div class="cameraOptHeader">Camera Options</div>
            <select v-model="selected">
                <option v-for="(cameraOption, idx) in cameraOptions" v-bind:value="cameraOption.value" :key="idx">
                    {{ cameraOption.value }}
                </option>
            </select>

            <button @click="getCameraImages">Select Camera</button>
        </div>
        <div v-if="yesImages" class="imageContainer">

            <div v-for="(imageResult, idx) in imageResults" :key="idx">
                <img :src="imageResult.img_src">
            </div>
        </div>

    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: 'forms',
        components: {},
        data() {
            return {
                imageCount: null,
                day: '3',
                month: '6',
                year: '2015',
                noImages: false,
                yesImages: false,
                selected: "FHAZ",
                imageResults: [],
                cameraOptions: [{
                        value: 'FHAZ'
                    },
                    {
                        value: 'RHAZ'
                    },
                    {
                        value: 'MAST'
                    },
                    {
                        value: 'CHEMCAM'
                    },
                    {
                        value: 'MAHLI'
                    },
                    {
                        value: 'MARDI',
                    },
                    {
                        value: 'NAVCAM'
                    },
                    {
                        value: 'PANCAM'
                    },
                    {
                        value: 'MINITIES',
                    }
                ],

            }
        },
        mounted() {},
        methods: {
            getResult(camera) {
                alert(camera)
            },

            getRoversByDateAndCamera() {
                axios.get('https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?earth_date=' + this.year +
                    '-' + this.month + '-' + this.day + '&api_key=mDHduMpjhX7nUwEdqNhG0RrlgrWUWkznF1R6sLmN').then(
                    response => {
                        const imagesQty = response.data.photos.length;
                        if (imagesQty > 0) {
                            this.yesImages = true;
                            this.noImages = false;
                            this.imageCount = imagesQty

                        } else {
                            this.noImages = true
                            this.yesImages = false;
                        }
                    });
            },

            getCameraImages() {
                axios.get(
                    'https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?&api_key=mDHduMpjhX7nUwEdqNhG0RrlgrWUWkznF1R6sLmN&earth_date=' +
                    this.year + '-' + this.month + '-' + this.day + '&camera=' + this.selected).then(response => {
                    this.imageResults = [];
                    response.data.photos.forEach(imageObject => {
                        this.imageResults.push(imageObject)
                    });
                })
            }

        }
    }
</script>

<style scoped>
    .datePicker {
        background-color: blue
    }

    .cameraOptHeader {
        margin-top: 3rem;
    }

    .noImages {
        font-weight: bold;
        color: red;
    }

    .imageContainer {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-template-rows: repeat(3, 1024px);
    }
</style>