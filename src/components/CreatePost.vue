<template>
    <div>
        <h1>Create Post</h1>
        <form class="form-horizontal">
            <div class="form-group">
                <label class="col-sm-2 control-label">Post title</label>
                <div class="col-sm-10">
                    <input v-model="title" type="text" class="form-control" placeholder="Post title">
                </div>
            </div>
            <transition name="component-fade" mode="out-in">
            <div v-if="title" class="form-group">
                <label class="col-sm-2 control-label">Post subtitle</label>
                <div class="col-sm-10">
                    <input type="text" class="form-control" placeholder="Post subtitle">
                </div>
            </div>
            </transition>
            <div class="form-group">
                <label class="col-sm-2 control-label">Post location</label>
                <div class="col-sm-10">
                    <input ref="autocomplete"
                           placeholder="Search"
                           class="form-control"
                           onfocus="value = ''"
                           type="text" />
                </div>
            </div>
            <transition name="component-fade" mode="out-in">
            <div v-if="Object.keys(place).length !== 0" class="form-group">
                <label class="col-sm-2 control-label">Post comment location</label>
                <div class="col-sm-10">
                    <!--<input type="text" class="form-control" placeholder="Post title">-->
                    <input type="text" class="form-control" placeholder="Post comment for location">
                </div>
            </div>
            </transition>
            <div class="form-group">
                <label class="col-sm-2 control-label">Post body</label>
                <div class="col-sm-10">
                    <textarea class="form-control" rows="5"></textarea>
                </div>
            </div>
            <div class="form-group">
                <div class="col-sm-offset-2 col-sm-10">
                    <button type="submit" class="btn btn-primary">Create</button>
                </div>
            </div>
        </form>
    </div>
</template>

<script>
    export default {
        name: "CreatePost",
        data () {
            return {
                title: '',
                place: {}
            }
        },
        mounted() {
            this.autocomplete = new google.maps.places.Autocomplete(
                (this.$refs.autocomplete),
                {types: ['geocode']}
            );

            this.autocomplete.addListener('place_changed', () => {
                this.place = this.autocomplete.getPlace();
                this.place.ac = this.place.address_components;
                // let lat = this.place.geometry.location.lat();
                // let lon = this.place.geometry.location.lng();
                // let city =  this.place.ac[0]["short_name"];
            });
        }
    }
</script>

<style scoped>
    .component-fade-enter-active, .component-fade-leave-active {
        transition: opacity .3s ease;
    }
    .component-fade-enter, .component-fade-leave-to
        /* .component-fade-leave-active below version 2.1.8 */ {
        opacity: 0;
    }
</style>