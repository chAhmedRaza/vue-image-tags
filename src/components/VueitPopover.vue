<template>
    <div class=""> 
        <div @click="triggerPopover">
            <slot name="popoverButton"></slot>   
        </div>
         
        <transition name="fade" appear>
            <div class="vueit-popover-container" v-if="isOpen">
                <slot name="popoverContent"></slot>
            </div>
        </transition> 
    </div> 
</template>    

<script>
export default {
    name: 'VitPopover',
    props: {
        isOpen: Boolean
    },
    methods: {
        triggerPopover(){
            this.$emit('triggerPopover');
        }
    }
}
</script>

<style scoped>
    .fade-enter-active, .fade-leave-active {
        transition: all .5s ease-out;
    }

    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
         opacity: 0;
    }
   
    .vueit-popover-container{
        position: absolute;
        background: white;
        padding: 10px;
        top: calc(100% + 18px);
        left: 50%;
        transform: translateX(-50%);
        width: max-content;
        border-radius: 5px;
        box-shadow: 0px 1px 20px 5px rgba(0,0,0,.2);
        z-index: 9999;
    }
</style>