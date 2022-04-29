<template>
    <div class="card">
        
        <Header :index="index" :nextIndex="nextIndex" :pages="pages" @hide="pageHided" />

        <Page :index="index" :nextIndex="nextIndex" :pages="pages" @goTo="goTo" @hide="pageHided" />

        <Footer :index="index" :nextIndex="nextIndex" :pages="pages" @home="goHome" @back="goBack" @forward="goForward" />

    </div>
</template>

<script>
import { gsap } from "gsap";
import Header from '@/components/Header.vue';
import Page from '@/components/Page.vue';
import Footer from '@/components/Footer.vue';

export default {
    name: "Card",
    components: {
        Header,
        Page,
        Footer
    },
    props: {
        msg: String,
    },
    data() {
        return {
            pages: [
                {
                    header: {
                        banner: '/main/top pic_01.png',
                        decor: '/main/home page_decor01.png',
                        decor_position: 'left',
                        header_icon: '',
                        header_title: ''
                    },
                    body: [
                        'home page_buttons01',
                        'home page_buttons02',
                        'home page_buttons03',
                        'home page_buttons04',
                        'home page_buttons05',
                        'home page_buttons06'
                    ]
                },
                {
                    header: {
                        banner: '/main/top pic_02.png',
                        decor: '/main/page_01_decor01.png',
                        decor_position: 'top_left',
                        header_icon: 'top icon_02',
                        header_title: 'Биотехнологии\nв прошлом'
                    },
                    body: [
                        'page_02_decor01',
                        'page_02_decor02',
                        'page_02_decor03'
                    ],
                    body_decor: 'page_01_decor02'
                },
                {
                    header: {
                        banner: '/main/top pic_03.png',
                        decor: '/main/page_03_decor01.png',
                        decor_position: 'top_left',
                        header_icon: 'top icon_03',
                        header_title: 'СЪЕДОБНЫЕ\nБИОТЕХНОЛОГИИ'
                    },
                    body: [
                        'page_03_decor01 (1)',
                        'page_03_decor02 (1)',
                        'page_03_decor03'
                    ]
                },
                {
                    header: {
                        banner: '/main/top pic_04.png',
                        decor: '/main/page_04_decor01.png',
                        decor_position: 'top_left',
                        header_icon: 'top icon_04',
                        header_title: 'Биотехнологическая\nаптека'
                    },
                    body: [
                        'page_04_decor01 (1)'
                    ]
                },
                {
                    header: {
                        banner: '/main/top pic_05.png',
                        decor: '',
                        decor_position: '',
                        header_icon: 'top icon_05',
                        header_title: 'БИОТЕХНОЛОГИИ\nИ ЗЕМНЫЕ НЕДРА'
                    },
                    body: [
                        'page_05_decor01 (1)',
                        'page_05_decor02',
                    ]
                },
                {
                    header: {
                        banner: '/main/top pic_06.png',
                        decor: '',
                        decor_position: '',
                        header_icon: 'top icon_06',
                        header_title: 'ОЧИСТКА ВОЗДУХА,\nВОДЫ И ПОЧВЫ'
                    },
                    body: [
                        'page_06_decor01',
                        'page_06_decor02',
                        'page_06_decor03'
                    ],
                    body_decor: 'page_07_decor02'
                },
                {
                    header: {
                        banner: '/main/top pic_07.png',
                        decor: '',
                        decor_position: '',
                        header_icon: 'top icon_07',
                        header_title: 'ВЗГЛЯД В БУДУЩЕЕ'
                    },
                    body: [
                        'page_07_decor01 (1)',
                        'page_07_decor02 (1)',
                        'page_07_decor03'
                    ],
                    body_decor: 'page_07_decor02'
                }
            ],
            currentPage: null,
            index: 0,
            nextIndex: 0,
            idleTimeout: null
        }
    },
    methods: {
        play() {
            this.hideInner();

            setTimeout(() => {
                this.currentPage = false;
                const tl = gsap.timeline({ repeat: 0, repeatDelay: 1 });
                
                tl.addLabel("start");
                
                //
                tl.to( ".gsap-el", { x: 0, opacity: 1, stagger: 0.1, duration: 0.35 } );
            }, 360 );

        },
        hide() {

            const tl = gsap.timeline({ repeat: 0, repeatDelay: 1 });
            tl.call(() => {
                
            });
            //
            tl.to( ".gsap-el", { x: 200, opacity: 0, stagger: 0.1, duration: 0.35 } );
            tl.call(() => {
                this.currentPage = true;
                setTimeout(() => {
                    this.playInner();
                }, 110)
                
            })
            
        },
        playInner() {
            this.currentPage = false;
            const tl = gsap.timeline({ repeat: 0, repeatDelay: 1 });
            tl.addLabel("start");
            //
            tl.to( ".pageEl", { x: 0, opacity: 1, stagger: 0.1, duration: 0.35 } );
        },
        hideInner() {
            const tl = gsap.timeline({ repeat: 0, repeatDelay: 1 });
            tl.call(() => {
                
            });
            //
            tl.to( ".pageEl", { x: 200, opacity: 0, stagger: 0.1, duration: 0.35 } );
            tl.call(() => {
                this.currentPage = true;
            })
        },
        goTo(page) {
            console.log({page});
            this.nextIndex = page;

            this.setIdle();
        },
        goHome() {
            this.nextIndex = 0;
            clearTimeout(this.idleTimeout);
        },
        goBack() {
            if(this.nextIndex === 0){
                return;
            }
            this.nextIndex -= 1;
            if(this.nextIndex === 0){
                clearTimeout(this.idleTimeout);
            }else{
                this.setIdle();
            }
        },
        goForward() {
            if(this.nextIndex >= this.pages.length - 1){
                return;
            }
            this.nextIndex += 1;
            this.setIdle();
        },
        pageHided() {
            this.index = this.nextIndex;
        },
        setIdle() {
            clearTimeout(this.idleTimeout);

            this.idleTimeout = setTimeout(() => {
                console.log('IDLE TIMEOUT!');

                this.nextIndex = 0;
            }, 60000);
        }
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
nav{
    position: fixed;
    right: 0;
    left: 0;
    top: 0;
    font-size: 24px;
    z-index: 999;
}
nav button{
    font-size: 24px;
}
.card{
    padding: 100px;
    /* padding-top: 86px; */
    position: relative;
    z-index: 5;
}
</style>
