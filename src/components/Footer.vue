<template>
    <footer class="footer">
        <nav>
            
            <div class="home_wrapper">
                <img src="/main/home page button active.png" :class="[homeVisibility ? 'opacity-visible' : '']" alt="">
                <img src="/main/home page button nonactive.png" class="opacity-visible" alt="">
                <button class="home_nav" @click="home" :disabled="homeVisibility ? false : true"></button>
            </div>
            
            <div class="back_wrapper">
                <!-- <img :src="prevIcon" alt=""> -->
                <img src="/main/back button active.png" :class="[prevVisibility ? 'opacity-visible' : '']" alt="" style="transform: translate(-1px, 0px);">
                <img src="/main/back button nonactive.png" class="opacity-visible" alt="">
                <button class="home_nav" @click="back" :disabled="prevVisibility ? false : true"></button>
            </div>

            <div class="forward_wrapper">
                <img src="/main/forward button active.png" :class="[nextVisibility ? 'opacity-visible' : '']" alt="" style="transform: translate(-3px, 0px);">
                <img src="/main/forward button nonactive.png" class="opacity-visible" alt="">
                <button class="home_nav" @click="forward" :disabled="nextVisibility ? false : true"></button>
            </div>

        </nav>
    </footer>
</template>

<script>
export default {
    name: 'Footer',
    props: {
        index: Number,
        nextIndex: Number,
        pages: Array
    },
    methods: {
        home() {
            this.$emit('home');
        },
        back() {
            this.$emit('back');
        },
        forward() {
            this.$emit('forward');
        }
    },
    computed: {
        prevVisibility() {
            if(this.index > 1) {
                return true;
            }else{
                return false;
            }
        },
        nextVisibility() {
            if(this.index < this.pages.length - 1 && this.index !== 0) {
                return true;
            }else{
                return false;
            }
        },
        homeVisibility() {
            if(this.index > 0) {
                return true;
            }else{
                return false;
            }
        }
    }
}
</script>

<style>
    .footer{
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        width: 100%;

        padding-bottom: 53px;
        padding-left: 57px;
    }
    .footer button{
        background: transparent;
        border: none;
        padding: 0;
        width: 60px;
        height: 60px;

        position: absolute;
    }
    .footer nav{
        display: flex;
    }
    .footer nav > div{
        display: flex;
        align-items: center;
        justify-content: center;
        position: relative;
    }

    .home_wrapper{
        transform: translate(4px, -5px);
        position: relative;
        width: 132px;
        height: 131px;
    }
    
    .back_wrapper{
        transform: translate(-7px, -5px);
        position: relative;
        width: 132px;
        height: 131px;
    }
    .forward_wrapper{
        transform: translate(-57px, -5px);
        position: relative;
        width: 132px;
        height: 131px;
    }

    .back_wrapper img,
    .home_wrapper img,
    .forward_wrapper img{
        transition: opacity 0.25s;
        opacity: 0;
        position: absolute;
        left: 0;
        top: 0;
    }

    .opacity-visible{
        opacity: 1!important;
    }
</style>