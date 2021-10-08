<template>
    <div class="home">

        <div class="box-gallery">
            <div class="container-fluid ">
                <div class="row mb-1">
                    <div class="col-3 p-0 mt-1 mb-1 slider">
                        <div class="row p-0">
                            <div v-for="image in images">
                                <img :key="image.id" :src="image.download_url" :alt="image.id" class="col-11">
                            </div>
                        </div>


                    </div>
                    <div class="col-9 p-0 mt-1 mb-1 screen">

                        <div class="show container">
                            <img src="../assets/johnny-depp-wallpaper-6-1600x1200.jpg" class="john" alt="6">

                        </div>


                    </div>
                </div>
            </div>
        </div>


    </div>
</template>

<script>
    // @ is an alias to /src
    import axios from 'axios';

    export default {
        name: 'Home',
        data() {
            return {
                images: []
            }
        },
        components: {},
        mounted: function () {
            axios.get("https://picsum.photos/v2/list?page=2&limit=100", {
                headers: {
                    'Authorization': 'Bearer' + 'Your Bearer Pssword',
                    "Content-Type": "application/json",
                }
            })
                .then(response => {
                    this.images = response.data
                    console.log(this.images);
                })
                .catch(function (error) {
                    console.log(error);
                });
        }
    }
</script>

<style>

    .box-gallery {
        height: 100vh;
    }

    .box-gallery .container-fluid {
        height: 100%;
        overflow-x: hidden;
    }

    .box-gallery .container-fluid .row {
        direction: rtl;
        height: 100%;
    }

    .box-gallery .container-fluid .row .slider {
        height: 100%;
        overflow-y: scroll;
        overflow-x: hidden;
        direction: rtl;
    }

    .box-gallery .container-fluid .row .slider .row {
        direction: ltr;
    }

    .box-gallery .container-fluid .row .screen {
        height: 100%;
    }

    .box-gallery .container-fluid .row .screen .show {
        height: 100%;
        width: 100%;
    }

    .box-gallery .container-fluid .row .screen .show .john {
        width: 90%;
        height: 700px;
        margin-right: 50px;
        margin-top: 20px;
    }

    ::-webkit-scrollbar {
        width: 5px;
    }

    /* Track */
    ::-webkit-scrollbar-track {
        background: none;
    }

    /* Handle */
    ::-webkit-scrollbar-thumb {
        background: rgba(0, 0, 255, 0.685);
    }

    /* Handle on hover */
    ::-webkit-scrollbar-thumb:hover {
        background: rgba(0, 0, 255, 0.685);
    }

    /*# sourceMappingURL=style.css.map */

</style>
