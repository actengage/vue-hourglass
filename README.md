# vue-hourglass

An SVG and CSS animated hourglass conveniently wrapped up in a Vue component.

![Screenshot](./img/hourglass.gif)

## Installation

    npm install vue-hourglass --save

## Basic Example

    <!-- in your main.js or equivelent -->
    import Hourglass from 'vue-hourglass';

    Vue.use(Hourglass);

    <!-- in the template... -->
    <hourglass animated />

## Examples

    <!-- Static Examples -->
    <hourglass label="Empty" empty />
    <hourglass label="Full" full />
    <hourglass label="Start" start />
    <hourglass label="Half" half />
    <hourglass label="End" end />

    <!-- Animated Examples -->
    <hourglass animated />
    <hourglass label="Loading..." animated />
