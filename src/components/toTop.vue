<template>
    <div class = "to-top" v-bind:class="show == true ? '' : 'to-top--hidden'" v-on:click="scrollToTop">
        <p>Scroll to top</p>
    </div>
</template>
<script>
export default {
    name: 'toTop',
    data() {
        return {
            show: false
        }
    },
    created () {
        // add an event listener for when the page is scrolled
        window.addEventListener('scroll', this.handleScroll);
    },
    methods: {
        // toggle the show state depending on whether the window has scrolled by 300px
        handleScroll() {
            if (window.pageYOffset > 300) {
                // if the page has scrolled by 300px show the button
                this.show = true;
            } else {
                // if the page hasn't scrolled by 300px hide the button
                this.show = false;
            }
        },
        scrollToTop() {
            // cause the page to scroll to the top of the page when the button is clicked
            window.scrollTo({
            top: 0,
            behavior: "smooth"
            });
        }
    }
}
</script>

<style lang="scss" scoped>
    .to-top {
        cursor: pointer;
        position: fixed;
        right: 1rem;
        bottom: 1rem;
        background: #f1c40f;
        padding: 1rem;
        color: white;
        transition: all 0.2s ease-in-out;

        p {
            margin: 0;
        }

        &--hidden {
            visibility: hidden;
            opacity: 0;
        }
    }
</style>