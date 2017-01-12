# simple-donut-jquery

This is a simple Donut and Pie chart function written in HTML/Sass/jQuery.

**For other simple donuts written in other JS libraries/frameworks, [go to the main repo](https://github.com/simple-donut/simple-donut.github.io).**

This repo produces this page:

* https://simple-donut.github.io/simple-donut-jquery

You can see a CodePen version here:

* http://codepen.io/TheJaredWilcurt/pen/wgGGjL

* * *

What you need for your project from this repo:

### HTML

You can change the `specificChart` id to any unique value. This allows you to target multiple donuts on the same page and to give them unique colors.

```html
<div id="specificChart" class="donut-size">
  <div class="pie-wrapper">
    <span class="label">
        <span class="num">0</span><span class="smaller">%</span>
    </span>
    <div class="pie">
      <div class="left-side half-circle"></div>
      <div class="right-side half-circle"></div>
    </div>
    <div class="shadow"></div>
  </div>
</div>
```

### Sass

This is completely customizable, but the main controls are right at the top in the variables.

```sass
$pie-size: 12em
$pie-main: hsl(168, 76%, 42%)
$pie-text: #7F8C8D
$pie-shadow: #BDC3C7

@import url('https://fonts.googleapis.com/css?family=Lato:700')

.donut-size
    font-size: $pie-size

.pie-wrapper
    position: relative
    width: 1em
    height: 1em
    margin: 0px auto
    font-family: 'Lato', Tahoma, Geneva, sans-serif
    .pie
        position: absolute
        top: 0px
        left: 0px
        width: 100%
        height: 100%
        clip: rect(0, 1em, 1em, 0.5em)
    .half-circle
        position: absolute
        top: 0px
        left: 0px
        width: 100%
        height: 100%
        border: 0.1em solid $pie-main
        border-radius: 50%
        clip: rect(0em, 0.5em, 1em, 0em)
        box-sizing: border-box
    .right-side
        transform: rotate(0deg)
    .label
        position: absolute
        top: 0.52em
        right: 0.4em
        bottom: 0.4em
        left: 0.4em
        display: block
        background: none
        border-radius: 50%
        color: $pie-text
        font-size: 0.25em
        line-height: 2.6em
        text-align: center
        cursor: default
        z-index: 2
    .smaller
        padding-bottom: 20px
        color: $pie-shadow
        font-size: .45em
        vertical-align: super
    .shadow
        width: 100%
        height: 100%
        border: 0.1em solid $pie-shadow
        border-radius: 50%
        box-sizing: border-box
```

### jQuery

This is the function that lets you update the values. It accepts selector for which donut chart to update, a number value for the percent, and a boolean for Donut or Pie chart.

```js
/**
 * Updates the donut chart's percent number and the CSS positioning of the progress bar.
 * Also allows you to set if it is a donut or pie chart
 * @param  {string}  el      The selector for the donut to update. '#thing'
 * @param  {number}  percent Passing in 22.3 will make the chart show 22%
 * @param  {boolean} donut   True shows donut, false shows pie
 */
function updateDonutChart (el, percent, donut) {
    percent = Math.round(percent);
    if (percent > 100) {
        percent = 100;
    } else if (percent < 0) {
        percent = 0;
    }
    var deg = Math.round(360 * (percent / 100));

    if (percent > 50) {
        $(el + ' .pie').css('clip', 'rect(auto, auto, auto, auto)');
        $(el + ' .right-side').css('transform', 'rotate(180deg)');
    } else {
        $(el + ' .pie').css('clip', 'rect(0, 1em, 1em, 0.5em)');
        $(el + ' .right-side').css('transform', 'rotate(0deg)');
    }
    if (donut) {
        $(el + ' .right-side').css('border-width', '0.1em');
        $(el + ' .left-side').css('border-width', '0.1em');
        $(el + ' .shadow').css('border-width', '0.1em');
    } else {
        $(el + ' .right-side').css('border-width', '0.5em');
        $(el + ' .left-side').css('border-width', '0.5em');
        $(el + ' .shadow').css('border-width', '0.5em');
    }
    $(el + ' .num').text(percent);
    $(el + ' .left-side').css('transform', 'rotate(' + deg + 'deg)');
}

// Update the chart
updateDonutChart('#specificChart', 66.67, true);
```
