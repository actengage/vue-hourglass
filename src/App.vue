<template>
    <div>
        <div class="container m-5">
            <h2>Static</h2>
            <hourglass :animate="false" label="Empty" empty class="p-3" />
            <hourglass :animate="false" label="Full" full class="p-3" />
            <hourglass :animate="false" label="Start" start class="p-3" />
            <hourglass :animate="false" label="Half" half class="p-3" />
            <hourglass :animate="false" label="End" end class="p-3" />
        </div>
        <div class="container m-5">
            <h2>Animated</h2>
            <hourglass class="p-3" />
            <hourglass label="Loading..." class="p-3" />
        </div>
    </div>
</template>

<script>
import Hourglass from './Hourglass';

export default {

    components: {
        Hourglass
    },

    data() {
        return {
            value: null
        };
    }

};
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap';
</style>
