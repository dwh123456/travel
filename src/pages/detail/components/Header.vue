<template>
    <div>
        <router-link 
            tag="div" to='/' 
            class="header-abs"
            v-show='showAbs'>
            <span class="iconfont header-abs-back" >&#xe624;</span>
        </router-link>
        <div 
            class="header-fixed" 
            v-show='!showAbs'
            :style='opacityStyle'>
            景点详情
            <router-link to="/">
                <div class="iconfont heider-fixed-back">&#xe624;</div>
            </router-link>
        </div>
    </div>
</template>

<script>
export default {
    name: 'DetailHeader',
    data () {
        return {
            showAbs: true,
            opacityStyle: {
                opacity: 0
            }
        }
    },
    methods: {
        handleScroll () {
            const top = document.documentElement.scrollTop
            console.log(top)
            if( top>60 ) {
                let opacity = top/140
                this.showAbs = false
                opacity = opacity> 1 ? 1: opacity
                this.opacityStyle = { opacity }
                
            } else {
                this.showAbs = true
            }
        }
    },
    activated () {
        window.addEventListener('scroll', this.handleScroll)
    },
    deactivated () {
        window.removeEventListener('scroll', this.handleScroll)
    }
}
</script>

<style lang='stylus' scoped>
@import '~styles/varibles.styl'
    .header-abs
        position: absolute
        left: .2rem
        top: .2rem
        width: .8rem
        height: .8rem
        border-radius: .4rem
        background: rgba(0, 0, 0, .8)
        text-align: center
        line-height: .8rem
        .header-abs-back
            color: #fff
            font-size: .4rem
    .header-fixed
        z-index: 2
        position fixed
        top: 0
        left: 0
        right: 0
        height: .86rem
        line-height: 0.86rem
        text-align: center
        color: #fff
        font-size: 0.32rem
        background: $bgColor
        .heider-fixed-back
            position: absolute
            top: 0
            left: 0
            width: .64rem
            text-align: center
            font-size: .4rem
            color: #fff
</style>

