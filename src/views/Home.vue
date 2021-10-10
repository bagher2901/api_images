<template>
    <div class="home">

        <div class="box-gallery">
            <div class="container-fluid ">
                <div class="row mb-1">
                    <div class="col-3 p-0 mt-1 mb-1 slider">
                        <div class="row p-0">
                            <div v-for="image in images">

                                    <img @click="atach_image(image.download_url)" :key="image.id" :src="image.download_url" :alt="image.id" class="p-1 image_list col-11">

                            </div>
                        </div>


                    </div>
                    <div class="col-9 p-0 mt-1 mb-1 screen">

                        <div class="show container">
                            <img v-if="first_or_next===true" :src="display_image" class="john" alt="6">
                            <img v-if="first_or_next===false" src="../assets/johnny-depp-wallpaper-26-1920x1080.jpg" class="john" alt="6">

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
                images: [],
                display_image:'',
                first_or_next:false
            }
        },
        methods:{
            atach_image:function (input) {

                this.first_or_next=true
                this.display_image = input;
                console.log(this.display_image)


            }

        },
        components: {},
        mounted: function () {

            axios.get("https://picsum.photos/v2/list?page=3&limit=100", {
                headers: {
                    'Authorization': 'Bearer' + 'Your Bearer Pssword',
                    "Content-Type": "application/json",
                }
            })
                .then(response => {
                    const {data} = response;
                    this.images = data;
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

    .image_list{
        opacity: 0.5;

    }
    .image_list:hover{
        opacity: 0.8;

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
        animation-duration: 3s;
        animation-name: john;
        border-radius: 15px;

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

    @keyframes john {
        from{
            opacity: 0;

        }
        to{
            opacity: 1;
        }


    }

    /*# sourceMappingURL=style.css.map */

</style>
