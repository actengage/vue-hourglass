<template>
    <div>
        <div class="container m-5">
            <h2>Static</h2>
            <hourglass label="Empty" empty class="p-3" />
            <hourglass label="Full" full class="p-3" />
            <hourglass label="Start" start class="p-3" />
            <hourglass label="Half" half class="p-3" />
            <hourglass label="End" end class="p-3" />
        </div>
        <div class="container m-5">
            <h2>Animated</h2>
            <hourglass animated class="p-3" />
            <hourglass animated label="Loading..." class="p-3" />
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
