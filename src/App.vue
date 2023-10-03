TODO: FIX BUG THAT DOESN'T LET ME ADD NEW PAGES
    bookmark: 2h28 on video
    bugfix: maybe aroun 2h25

<template>
    <navbar 
    :pages="pages"
    :active-page="activePage"
    ></navbar>

<div v-show="false"></div>

    <page-viewer
    v-if="pages.length > 0"
    :page="pages[activePage]"></page-viewer>

    <create-page
    @page-created="pageCreated"
    ></create-page>

</template>

<script>
import Navbar from './components/Navbar.vue'
import PageViewer from './components/PageViewer.vue';
import CreatePage from './components/CreatePage.vue';

export default {
    components: {
        Navbar,
        PageViewer,
        CreatePage

    },
    created(){
        // Created gets called before the components are loaded in, allowing for data to be processed before loading components that might use it.
        this.getPages();

        this.$bus.$on('navbarLinkActivated', (index) =>{
            this.activePage = index;
        });
    },
    data() {
        // to decide when to load data it's good to assess if the data is going to be used by
        // multiple components or just a single component
        return {
            activePage: 0,
            pages: []
        };
    },
    methods:{
        async getPages(){
            let res = await fetch('pages.json')
            let data = await res.json();

            this.pages = data;
        },
        pageCreated(pageObj){
            this.pages.push(pageObj);
        }
    }
}

</script>