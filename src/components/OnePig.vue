<template>
    <div>
        <input type="checkbox" :id="id" :checked="isEat" @change="$emit('checkbox-changed')"/>
        <label for="little-pig">{{selfIntroduce}}</label>
    </div>
</template>
<script>
    export default {
        props: {
            selfIntroduce: { required: true, type: String},
            eat: {default: false, type: Boolean},
            id: {required: true, type: String},
        },
        data() {
            return {
                isEat: this.eat,
            }
        }
    }
</script>