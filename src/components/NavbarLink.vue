<template>
    <a 
    class="nav-link"
    :class="activeClasses"
    aria-current="page"
    :href="page.link.url"
    >{{ page.link.text }}</a>
    <!-- v-on:click or @click can be used here, they do the same thing  -->
</template>

<script>
export default {
    props: ['page', 'isActive'],
    computed: {
        activeClasses() {
            return {
                active: this.isActive,
                emphasize: this.isActive
            };
        }
    }
}
</script>

<style scoped>
.emphasize{
    text-decoration: underline !important;
}

/* a scoped style only applies to the component it is placed in.
If scoped is not inserted, it can apply to different components. */
</style>