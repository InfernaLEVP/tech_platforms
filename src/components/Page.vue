<template>
    <main class="page">
        
        <div class="page_wrapper">
            <img 
                v-for="(image, index) in pageContent" 
                :key="image" 
                :src="`/main/${image}.png`" 
                class="gsap-page-el" 
                @click="goTo(index + 1)"
            />
        </div>

        <img v-if="bodyDecor" :src="bodyDecor" class="body_decor gsap-page-el">

    </main>
</template>

<script>
import { gsap } from "gsap";

export default {
    name: 'Page',
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
                tl.to( ".gsap-page-el", { x: 0, opacity: 1, stagger: 0.1, duration: 0.35 } );
            }, 340 );

        },
        hide() {
            return new Promise((resolve, reject) => {
                const tl = gsap.timeline({ repeat: 0, repeatDelay: 1 });
                
                tl.to( ".gsap-page-el", { x: 200, opacity: 0, stagger: 0.1, duration: 0.25 } );
                tl.call(() => {
                    resolve();
                })
            });
            
        },
        goTo(num) {
            if(this.index === 0){
                this.$emit('goTo', num);
            }
        }
    },
    computed: {
        pageContent() {
            return this.pages[this.index].body;
        },
        bodyDecor() {
            if(this.pages[this.index].body_decor){
                return `/main/${this.pages[this.index].body_decor}.png`;
            }else{
                return false;
            }
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
    .gsap-page-el{
        transform: translateX(270px);
        opacity: 0;
    }

    .page{

    }
    .page_wrapper{

    }
    .page_wrapper img{
        margin-bottom: 38px;
    }
    .body_decor{
        position: absolute;
        right: 50px;
        top: 1750px;
    }
</style>