<template>
<div class="col-body">
    <transition-group class="col-body-section" name="list-complete" tag="ul" v-on:before-enter="beforeEnter" v-on:enter="enter"
    v-on:after-enter="afterEnter" v-on:before-leave="beforeLeave" v-on:leave="leave" v-on:after-leave="afterLeave">
    <a class="col-body-item" v-for="(item, index) in currentBookMarks" :key="new Date()*1" v-bind:data-index="index+1" :id="'item_' + index " :href="item.url" target="_blank" >
        <div class="icon icon-img" v-if="item.icon && item.icon.match(/^[\w]+\:\/\//)">
        <img :src="item.icon" alt="">
        </div>
        <div class="icon icon-font" v-else-if="item.icon">
        <i class="fa" :class="[item.icon]"></i>
        </div>
        <div class="icon icon-text" v-else>
        <span>{{item.name[0]}}</span>
        </div>
        <div class="name">
        {{item.name}}
        </div>
    </a>
    </transition-group>
</div>
</template>
<style lang="less" scoped>
.col-body {
    position: absolute;
    top: 80px;
    left: 50%;
    width: 1000px;
    transform: translateX(-50%);
}
.col-body-section {
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
    position: relative;
}
.col-body-item {
    width: 200px;
    height: 200px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    transition: all 0.3s;
    cursor: pointer;
    text-decoration: none;
    &:hover {
        transform: scale(1.2) !important;
    }
    .icon {
        width: 100px;
        height: 100px;
        display: flex;
        justify-content: center;
        align-items: center;
        &.icon-img {
            border-radius: 100%;
            img {
                width: 100px;
                height: 100px;
                border-radius: 100%;
            }
        }
        &.icon-text,
        &.icon-font {
            border-radius: 100%;
            background: #ccc;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 60px;
            color: #666;
            box-shadow: 0px 0px 1px rgba(0, 0, 0, 0.1),
                0px 2px 1px rgba(0, 0, 0, 0.1);
            background: #fff;
        }
    }
    .name {
        color: #fff;
        padding-top: 20px;
        text-align: center;
        text-shadow: 0 0 2px #cacaca;
    }
}
</style>

<script>
export default {
    props: ['currentBookMarks'],
    data() {
        return {};
    },
    computed: {},
    mounted() {},
    methods: {
        beforeEnter(el) {
            console.log('beforeEnter', el.id);
            el.style.opacity = 0;
            el.style.transform = 'translateY(' + 100 + 'px)';
            el.style.transitionDelay = el.dataset.index * 0.04 + 's';
        },
        enter(el) {
            console.log('enter', el.id);
        },
        afterEnter(el) {
            console.log('afterEnter', el.id);
            el.style.opacity = 1;
            el.style.transform = 'translateY(' + 0 + 'px)';
        },
        beforeLeave(el) {
            console.log('beforeLeave', el.id);
            el.style.left = el.offsetLeft + 'px';
            el.style.top = el.offsetTop + 'px';
            el.style.opacity = 1;
            el.style.transform = 'translateY(' + 0 + 'px)';
            el.style.transitionDelay = 0 + 's';
            setTimeout(() => {
                el.style.position = 'absolute';
            });
        },
        leave(el) {
            console.log('leave', el.id);
            el.style.opacity = 0;
            el.style.transform = 'translateY(' + 100 + 'px)';
        },
        afterLeave(el) {
            console.log('afterLeave', el.id);
        }
    }
};
</script>
