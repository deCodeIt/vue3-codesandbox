<template>
    <div class="item-container" >
        <input type="checkbox" v-model="checked" />
        <p> {{ title }} </p>
        <button @click="deleteEle" >x</button>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    props: {
        title: {
            type: String,
            required: true,
        },
        isChecked: {
            type: Boolean,
            required: true,
        }
    },
    data() {
        return {
            checked: this.isChecked,
        }
    },
    watch: {
        checked( newVal ) {
            this.$emit( 'checkevent', newVal );
        }
    },
    methods: {
        deleteEle() {
            console.log('delete');
            this.$emit( 'deleteevent' );
        }
    }
})
</script>

<style scoped>
.item-container {}

.delete {
    color: red;
}
</style>