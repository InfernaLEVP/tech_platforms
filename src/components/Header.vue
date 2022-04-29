<template>
    <header class="header">

        <div class="header_title" v-if="pageContent.header.header_title">
            <img class="gsap-header-el" :src="`/main/${pageContent.header.header_icon}.png`">
            <h2 class="gsap-header-el" v-html="lineBreaks(pageContent.header.header_title)"></h2>
        </div>

        <div :class="['header_wrapper', 'gsap-header-el', index === 0 ? 'home' : 'inner' ]">
            <img :src="pageContent.header.banner" class="header_main">

            <img :src="pageContent.header.decor" :class="['header_decor', pageContent.header.decor_position ]">
        </div>

    </header>
</template>

<script>
import { gsap } from "gsap";

export default {
    name: 'Header',
    props: {
        index: Number,
        nextIndex: Number,
        pages: Array
    },
    data() {
        return {

        }
    },
    mounted() {
        setTimeout(() => {
            this.play();
        }, 40);
    },
    methods: {
        play() {

            setTimeout(() => {
                
                const tl = gsap.timeline({ repeat: 0, repeatDelay: 1 });
                
                tl.addLabel("start");
                
                //
                tl.to( ".gsap-header-el", { x: 0, opacity: 1, stagger: 0.1, duration: 0.35 } );
            }, 40 );

        },
        hide() {
            return new Promise((resolve, reject) => {
                const tl = gsap.timeline({ repeat: 0, repeatDelay: 1 });
                
                tl.to( ".gsap-header-el", { x: 200, opacity: 0, stagger: 0.1, duration: 0.25 } );
                tl.call(() => {
                    resolve();
                })
            });
            
        },
        lineBreaks(text) {
            return text.replaceAll('\n', '<br>');
        }
    },
    computed: {
        pageContent() {
            return this.pages[this.index];
        }
    },
    watch: {
        nextIndex(newValue, oldValue) {
            const hide = this.hide();
            hide.then(() => {
                this.$emit('hide');
            });
        },
        index(newValue, oldValue) {
            this.play();
        }
    }
}
</script>

<style>
.header{
    position: relative;
}   

.header_wrapper{

}

.gsap-header-el{
    transform: translateX(200px);
    opacity: 0;
}

.header_main{
    width: 100%;
    max-width: 100%;
    transform: none;
}
.home .header_main{
    width: 111%;
    max-width: 111%;
    transform: translate(-21px, -10px);
}
.inner .header_main{
    width: 103.5%;
    max-width: 103.5%;
    transform: translate(-21px, -10px);
}

.header_decor{
    position: absolute;
    z-index: -1;
}
.header_decor.left{
    left: -180px;
    top: 71px;
    z-index: 65;
}
.header_decor.top_left{
    right: -100px;
    top: -691px;
}

.header_title{
    display: flex;
    align-items: center;
    font-size: 33px;
    color: white;
    text-transform: uppercase;

    position: relative;
    z-index: 55;
    font-family: 'Grandis-Bold', sans-serif;
}
.header_title h2{
    margin: 0;
    font-size: 36px;
    line-height: 1.1;
}
.header_title img{
    margin-right: 37px;
}
.header_title+.header_wrapper{
    margin-top: 50px;
}

</style>