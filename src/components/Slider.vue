<script>

export default{
    data(){
        return{
            activeImage:0,
            sliderImg:[
                {
                    url:'h-2-slider-img-11.png',
                },
                {
                    url:'h-2-slider-img-15.png',
                    url2:'h-2-slider-img-16.png',
                },
                {
                    url:'short-slider-rev-1-img-3.png'
                }
                
            ],
            backImages:[
                {
                    url:'h-2-slider-img-12.png',
                    cls:'slider-1'
                },
                {
                    url:'h-2-slider-img-13.png',
                    cls:'slider-2'
                },
                {
                    url:'h-2-slider-img-14.png',
                    cls:'slider-3'
                },
                {
                    url:'short-slider-rev-1-img-2.png',
                    cls:'slider-4'
                },
                {
                    url:'short-slider-rev-1-img-6.png',
                    cls:'slider-5'
                },
                {
                    url:'h-2-slider-img-17.png',
                    cls:'slider-6'
                },
            ]
        }
    },
    methods: {
        goToPrev(){
            this.activeImage--;
            if(this.activeImage < 0){
                this.activeImage = this.sliderImg.length - 1;
            }
        },
        goToNext(){
            this.activeImage++;
            if(this.activeImage == this.sliderImg.length){
                this.activeImage = 0;
            }
        },
        changeImage(index){
            this.activeImage = index
        },
        getImagePath: function(img){
            return new URL(`../assets/${img}`, import.meta.url).href;
        }
    }
}

</script>

<template>
    <div class="container">

        <div>
            <div class="prevImg" @click="goToPrev"><i class="fa-solid fa-arrow-left"></i></div>
            <div class="nextImg" @click="goToNext"><i class="fa-solid fa-arrow-right"></i></div>
        </div>

        <div class="introdution">
            <h1>Devotion that never <span><i>ends</i></span></h1>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vel, adipisci quisquam animi distinctio hic dicta dolore fugiat.</p>
            <button>READ MORE</button>
        </div>
        <div class="img-wrap">

            <div class="slider-short">
                <img v-for='image in backImages' :src="getImagePath(image.url)" alt="slider img" :class="image.cls">
            </div>

            <div class="image">
                <img :src="sliderImg[activeImage].url" :class="activeImage==1?'img2':'img'">
                <img v-show='activeImage == 1' :src="sliderImg[activeImage].url2" class="img2">
            </div>

        </div>

    </div>

    <div class="thumb-cnt">
        <div class="thumb" v-for="thumb,index in sliderImg" @click="changeImage(index)" :class="(activeImage==index)?'active':''"></div>
    </div>

</template>

<style scoped lang="scss">
@use '../styles/general.scss' as *;
@use '../styles/partial/variables.scss' as *;
@use '../styles/partial/-mixin.scss' as *;
.container{
    @include my-container;
    display: flex;
    height: 500px;

    .introdution {
        width: 40%;
    }

    .img-wrap {
        width: 60%;
        position: relative;

        .slider-short{
            img{
                position: absolute;
            }

            .slider-1{
                top: 50%;
                transform:translateY(-50%) ;
            }
            .slider-2{
                bottom: 0;
                left: 30px;
            }
            .slider-3{
                left: 80%;
            }

            .slider-4{
                left: 10%;
            }
            .slider-5{
                right: 0;
                top: 30%;
            }
            .slider-6{
                bottom: 0;
                right: 0;
            }
        }
    }

    .image{
        width: 100%;
        height: 100%;
        padding: 3rem;

        .img{
            object-fit: contain;
            width: 100%;
            height: 100%;
        }

        .img2{
            width: 50%;
            object-fit: contain;
            padding-top: 3rem;
            display: inline-block;
        }
    }

    h1{
        font-size: 4rem;
        font-weight: 300;
        
        span{
            font-family: 'Dancing Script', cursive;
            font-weight: bolder;
        }
    }

    p{
        opacity: 0.5;
        padding: 2rem 0;
    }
}

.prevImg, .nextImg{
    @include my-display-flex;
    width: 30px;
    height: 30px;
    justify-content: center;
    background-color: $back-10;
    border-radius: 50%;
    position: absolute;  
    top: 50%;
    transform: translateY(-50%);
}

.prevImg{
    left: 50px;
}

.nextImg{
    right: 50px;
}

.thumb-cnt{
    display: flex;
    justify-content: center;
    padding: 2rem 0;

    .thumb{
        width: 10px;
        height: 10px;
        border-radius: 50%;
        background-color: $back-10;
        margin: 0 0.5rem;
    }
}
.active{
    transform: scale(1.5);
}

button{
    padding: 1rem;
    background: none;
    border: none;
    border: 2px solid $border-color-4;
    font-size: 12px;
    font-weight: bold;
    letter-spacing: 2px;

    &:hover{
        background-color: $border-color-4;
        transition: all 2s ease;
    }

}

</style>