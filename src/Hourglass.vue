<template>
    <div class="hourglass" :class="classes" :style="{animationDuration: `${this.duration}ms`}">
        <div class="hourglass-icon">
            <div class="hourglass-empty">
                <icon :icon="['far', 'hourglass']" />
            </div>
            <div class="hourglass-full">
                <icon icon="hourglass" />
            </div>
            <div class="hourglass-start">
                <icon icon="hourglass-start" />
            </div>
            <div class="hourglass-half">
                <icon icon="hourglass-half" />
            </div>
            <div class="hourglass-end">
                <icon icon="hourglass-end" />
            </div>
        </div>
        <div v-if="label" class="hourglass-label">{{ label }}</div>
    </div>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core';
import { FontAwesomeIcon as Icon } from '@fortawesome/vue-fontawesome';
import { faHourglass } from '@fortawesome/free-regular-svg-icons';
import { faHourglassStart, faHourglassHalf, faHourglassEnd, faHourglass as faHourglassFull } from '@fortawesome/free-solid-svg-icons';

library.add(faHourglass);
library.add(faHourglassEnd);
library.add(faHourglassHalf);
library.add(faHourglassStart);
library.add(faHourglassFull);

export default {

    name: 'Hourglass',

    components: {
        Icon
    },

    props: {

        empty: Boolean,

        start: Boolean,

        half: Boolean,

        end: Boolean,

        full: Boolean,

        animate: {
            type: Boolean,
            default: false
        },

        duration: {
            type: Number,
            default: 4000
        },

        label: {
            type: String
        },

    },

    methods: {

        startAnimation() {
            this.stopAnimation();

            this.interval = setInterval(() => {
                this.rotate = !this.rotate
            }, this.duration / 2);
        },

        stopAnimation() {
            if(this.interval) {
                clearInterval(this.interval);
            }
        }
    },

    watch: {
        animate(value) {
            value && this.startAnimation();
        }
    },

    computed: {
        
        classes() {
            return {
                'hourglass-animate': this.animate,
                'hourglass-empty': this.empty,
                'hourglass-rotate': this.rotate,
                'hourglass-start': this.start,
                'hourglass-half': this.half,
                'hourglass-end': this.end,
                'hourglass-full': this.full
            };
        }

    },

    mounted() {
        if(this.animate) {
            this.startAnimation();
        }
    },

    data() {
        return {
            rotate: false,
            interval: null
        };
    }

}
</script>

<style lang="scss">
@import 'bootstrap/scss/_functions.scss';
@import 'bootstrap/scss/_variables.scss';

@keyframes hourGlassStart {
    0% { opacity: 1; }
    15% { opacity: 1; }
    25% { opacity: 0; }
    50% { opacity: 0; }
    75% { opacity: 0; }
    85% { opacity: 1; }
    100% { opacity: 1; }
}

@keyframes hourGlassHalf {
    0% { opacity: 0; }
    25% { opacity: 1; }
    50% { opacity: 0; }
    75% { opacity: 1; }
    100% { opacity: 0; }
}

@keyframes hourGlassEnd {
    0% { opacity: 0; }
    25% { opacity: 0; }
    50% { opacity: 1; }
    75% { opacity: 0; }
    100% { opacity: 0; }
}

@keyframes hourGlassRotate {
    0% { transform: rotate(0deg); }
    90% { transform: rotate(0deg); }
    100% { transform: rotate(180deg); }
}

.hourglass {
    align-items: center;
    display: inline-flex;
    flex-direction: column;
    justify-content: center;

    &.hourglass-animate.hourglass-rotate .hourglass-icon {
        transform: rotate(180deg);
    }

    &:not(.hourglass-animate) {
        .hourglass-half {
            opacity: 1;
        }
    }

    .hourglass-label {
        font-size: .9em;
        padding-top: .333em;
    }

    .hourglass-icon {
        width: 1em;
        height: 1em;
        font-size: 2rem;
        position: relative;
        animation-duration: inherit;
        transition: transform .2s ease-in;

        & > div {
            left: 50%;
            top: 50%;
            opacity: 0;
            position: absolute;
            transform: translate(-50%, -50%);
            animation-duration: inherit;
            animation-fill-mode: forwards;
            animation-iteration-count: infinite;
        }  
    }  
    
    &.hourglass-animate .hourglass-empty {
        opacity: 1;
    }
        
    &.hourglass-animate .hourglass-start {
        z-index: 3;
        animation-name: hourGlassStart;
    }
    
    &.hourglass-animate .hourglass-half {
        z-index: 2;
        animation-name: hourGlassHalf;
    }
    
    &.hourglass-animate .hourglass-end {
        z-index: 1;
        animation-name: hourGlassEnd;
    } 
    
    &:not(.hourglass-animate) {
    
        .hourglass-empty,
        .hourglass-start,
        .hourglass-half,
        .hourglass-end,
        .hourglass-full {
            opacity: 0;
        }

        &.hourglass-empty .hourglass-empty,
        &.hourglass-start .hourglass-start,
        &.hourglass-half .hourglass-half,
        &.hourglass-end .hourglass-end,
        &.hourglass-full .hourglass-full {
            opacity: 1;
        }
    }
}
</style>
