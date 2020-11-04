<template>
    <transition name="fade">
        <div class="back-top" :style="style" v-if="visible" @click="handleBackTop">
            <slot>
                <div class="wrapper" :style="wrapperStyle">
                    <div class="top"></div>
                </div>
            </slot>
        </div>
    </transition>
</template>

<script>
// 防抖函数
function debounce(func, wait = 0) {
    let timer = null;
    return function() {
        const context = this
        const args = arguments
        if (!timer) {
            timer = setTimeout(function() {
                func.apply(context, args)
                timer = null
            }, wait)
        }
    }
}

export default {
    props: {
        width: {
            type: Number,
            default: 64
        },
        height: {
            type: Number,
            default: 64
        },
        offsetX: {
            type: Number,
            default: 50
        },
        offsetY: {
            type: Number,
            default: 50
        },
        circle: {
            type: Boolean,
            default: true
        },
        delay: {
            type: Number,
            default: 250
        }
    },
    data() {
        return {
            viewHeight: 0,
            scrollTop: 0
        }
    },
    mounted() {
        this.viewHeight = document.documentElement.clientHeight
        window.addEventListener('scroll', this.onScroll)
        this.$once('hook:beforeDestroy', () => {
            window.removeEventListener('scroll', this.onScroll)
        })
    },
    computed: {
        visible() {
            return this.scrollTop > this.viewHeight
        },
        style() {
            return {
                width: this.width + 'px',
                height: this.height + 'px',
                right: this.offsetX + 'px',
                bottom: this.offsetY + 'px',
            }
        },
        wrapperStyle() {
            return {
                borderRadius: this.circle ? '50%' : '0'
            }
        }
    },
    methods: {
        onScroll: debounce(function() {
            this.scrollEvent()
        }, 100),
        scrollEvent() {
            this.scrollTop = document.documentElement.scrollTop
        },
        handleBackTop() {
            const stepTime = 10
            const steps = this.delay / stepTime
            const stepDistance = steps === 0 ? document.documentElement.scrollTop / stepDistance : document.documentElement.scrollTop
            const timer = setInterval(() => {
                const scrollTop = document.documentElement.scrollTop
                if (scrollTop <= 0) {
                    clearInterval(timer)
                }
                else {
                    document.documentElement.scrollTop -= stepDistance
                }
            }, stepTime)
        }
    }
}
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
    opacity: 0;
}

.back-top {
    position: fixed;
    z-index: 10000;
    cursor: pointer;
}
.wrapper {
    width: 100%;
    height: 100%;
    background-color: rgba(100, 100, 100, 0.7);
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 12px;
    color: #fff;
}
.wrapper:hover, .wrapper:active {
    background-color: rgba(100, 100, 100, 0.9);
}
.top {
    border-bottom: 8px solid #fff;
    border-left: 8px solid transparent;
    border-right: 8px solid transparent;
}
</style>
