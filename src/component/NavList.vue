<template>
<div class="col-nav">
    <!-- <div class="col-nav-logo">Google123</div> -->
    <div class="col-nav-all" >
        <div   v-for="(value, index) in data" :key="index" class="col-nav-item" :class="{'selected': index == selected }"
        @click="selectEvent(index)">
            {{value.slice(0, -5)}}
        </div>
    </div>
</div>
</template>
<style lang="less" scoped>
.col-nav {
    position: absolute;
    width: 100%;
    left: 80px;
    top: 5px;
    .col-nav-all {
        display: flex;
        justify-content: flex-start;
    }
    .col-nav-item {
        position: relative;
        margin-right: 30px;
        cursor: pointer;
        color: #fff;
        &.selected::before {
            position: absolute;
            bottom: -5px;
            left: 50%;
            content: '';
            width: 15px;
            height: 3px;
            border-radius: 10px;
            background-color: rgba(255, 255, 255, 0.6);
            margin-left: -7.5px;
        }
    }
}
</style>
<script>
export default {
    props: ['data'],
    data() {
        return {
            selected: 0
        };
    },
    mounted() {
        this.$emit('selected', this.data[0]);
    },
    methods: {
        selectEvent(index) {
            var key = this.data[index];
            this.selected = index;
            this.$emit('selected', key);
        }
    }
};
</script>
