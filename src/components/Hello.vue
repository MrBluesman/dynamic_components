<template>
    <div>
        <div class="header clearfix">
            <nav>
                <ul class="nav nav-pills pull-right">
                    <li role="presentation">
                        <a href="#" v-on:click="currentView='ManagePosts'">Manage Posts</a>
                    </li>
                    <li role="presentation">
                        <a href="#" v-on:click="currentView='CreatePost'">Create Post</a>
                    </li>
                    <li role="presentation">
                        <a href="#" v-on:click="currentView='Location'">Location</a>
                    </li>
                </ul>
            </nav>
            <h3 class="text-muted">Admin Panel</h3>
        </div>

        <div class="container">
            <keep-alive>
                <transition name="component-fade" mode="out-in">
                    <component v-bind:is="currentView"></component>
                </transition>
            </keep-alive>
        </div>
    </div>
</template>

<script>
    import ManagePosts from "./ManagePosts";
    import CreatePost from "./CreatePost";
    import Location from "./Location";

    export default {
        name: "Hello",
        data () {
            return {
                currentView: 'ManagePosts'
            }
        },
        components: {ManagePosts, CreatePost, Location}
    }
</script>

<style scoped>
    .header {
        padding: 15px 15px 20px 15px;
        border-bottom: 1px solid #e5e5e5;
    }

    .header h3 {
        margin-top: 0;
        margin-bottom: 0;
        line-height: 40px;
    }

    .component-fade-enter-active, .component-fade-leave-active {
        transition: opacity .3s ease;
    }
    .component-fade-enter, .component-fade-leave-to
        /* .component-fade-leave-active below version 2.1.8 */ {
        opacity: 0;
    }
</style>