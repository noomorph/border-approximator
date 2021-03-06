# What does it solve?

There is a transparent borderless *Button A* which is styled using `box-shadow` CSS property.
You have to create *Button B* which should look as similar as possible to *Button A* without using `box-shadow`.
Unfortunately, the only CSS properties you can use are either `border` or `outline`.

In our days it is common to search answers or ask smart people on **StackOverflow**, [but sometimes nobody is interested or able to answer your question, like in my case](https://stackoverflow.com/questions/48097129/how-to-approximate-css-box-shadow-property-using-solid-border-only).
Fortunately, I had some time and luck to conduct my own research and you came here in time, when I've got some useful results for you.

### Demo

<iframe id="demo-iframe" src="demo/index.html?rnd=5" width="100%" height="460" allowtransparency="true" frameborder="0" scrolling="no"></iframe>

### The Useful Code

```javascript
const SHADOW_APPROXIMATION_MAP = [
              /*blur=00*/ /*blur=01*/ /*blur=02*/ /*blur=03*/ /*blur=04*/ /*blur=05*/ /*blur=06*/ /*blur=07*/ /*blur=08*/ /*blur=09*/ /*blur=10*/ /*blur=11*/ /*blur=12*/ /*blur=13*/ /*blur=14*/ /*blur=15*/
/* size=00 */ [ 0, 0.00], [ 1, 0.27], [ 1, 0.32], [ 1, 0.35], [ 2, 0.27], [ 2, 0.30], [ 2, 0.32], [ 3, 0.27], [ 3, 0.29], [ 3, 0.30], [ 3, 0.31], [ 4, 0.27], [ 4, 0.28], [ 4, 0.29], [ 4, 0.30], [ 5, 0.27],
/* size=01 */ [ 1, 1.00], [ 1, 0.73], [ 2, 0.49], [ 2, 0.49], [ 2, 0.48], [ 2, 0.48], [ 3, 0.40], [ 3, 0.40], [ 3, 0.41], [ 4, 0.35], [ 4, 0.36], [ 4, 0.37], [ 4, 0.37], [ 5, 0.33], [ 5, 0.34], [ 5, 0.35],
/* size=02 */ [ 2, 1.00], [ 2, 0.86], [ 2, 0.78], [ 3, 0.60], [ 3, 0.59], [ 3, 0.57], [ 3, 0.56], [ 4, 0.47], [ 4, 0.47], [ 4, 0.47], [ 4, 0.47], [ 5, 0.42], [ 5, 0.42], [ 5, 0.42], [ 5, 0.42], [ 6, 0.38],
/* size=03 */ [ 3, 1.00], [ 3, 0.91], [ 3, 0.85], [ 3, 0.81], [ 4, 0.67], [ 4, 0.65], [ 4, 0.63], [ 4, 0.62], [ 5, 0.53], [ 5, 0.53], [ 5, 0.52], [ 5, 0.51], [ 5, 0.51], [ 6, 0.46], [ 6, 0.46], [ 6, 0.45],
/* size=04 */ [ 4, 1.00], [ 4, 0.93], [ 4, 0.89], [ 4, 0.85], [ 4, 0.82], [ 5, 0.71], [ 5, 0.69], [ 5, 0.67], [ 5, 0.65], [ 5, 0.64], [ 6, 0.57], [ 6, 0.56], [ 6, 0.55], [ 6, 0.55], [ 7, 0.50], [ 7, 0.49],
/* size=05 */ [ 5, 1.00], [ 5, 0.94], [ 5, 0.91], [ 5, 0.88], [ 5, 0.86], [ 5, 0.83], [ 6, 0.73], [ 6, 0.71], [ 6, 0.70], [ 6, 0.68], [ 6, 0.67], [ 7, 0.60], [ 7, 0.59], [ 7, 0.58], [ 7, 0.58], [ 8, 0.53],
/* size=06 */ [ 6, 1.00], [ 6, 0.95], [ 6, 0.92], [ 6, 0.90], [ 6, 0.88], [ 6, 0.85], [ 7, 0.76], [ 7, 0.75], [ 7, 0.73], [ 7, 0.72], [ 7, 0.70], [ 7, 0.69], [ 8, 0.63], [ 8, 0.62], [ 8, 0.61], [ 8, 0.60],
/* size=07 */ [ 7, 1.00], [ 7, 0.96], [ 7, 0.93], [ 7, 0.91], [ 7, 0.89], [ 7, 0.87], [ 7, 0.85], [ 8, 0.78], [ 8, 0.76], [ 8, 0.75], [ 8, 0.73], [ 8, 0.72], [ 8, 0.71], [ 9, 0.65], [ 9, 0.64], [ 9, 0.63],
/* size=08 */ [ 8, 1.00], [ 8, 0.96], [ 8, 0.94], [ 8, 0.92], [ 8, 0.91], [ 8, 0.89], [ 8, 0.87], [ 8, 0.85], [ 9, 0.78], [ 9, 0.77], [ 9, 0.76], [ 9, 0.75], [ 9, 0.73], [ 9, 0.72], [10, 0.67], [10, 0.65],
/* size=09 */ [ 9, 1.00], [ 9, 0.96], [ 9, 0.95], [ 9, 0.93], [ 9, 0.91], [ 9, 0.90], [ 9, 0.89], [ 9, 0.87], [10, 0.80], [10, 0.79], [10, 0.78], [10, 0.77], [10, 0.75], [10, 0.75], [10, 0.73], [11, 0.68],
/* size=10 */ [10, 1.00], [10, 0.97], [10, 0.95], [10, 0.94], [10, 0.92], [10, 0.91], [10, 0.89], [10, 0.88], [10, 0.87], [11, 0.81], [11, 0.80], [11, 0.78], [11, 0.77], [11, 0.76], [11, 0.75], [11, 0.74],
/* size=11 */ [11, 1.00], [11, 0.97], [11, 0.95], [11, 0.94], [11, 0.93], [11, 0.92], [11, 0.90], [11, 0.89], [11, 0.88], [12, 0.82], [12, 0.81], [12, 0.80], [12, 0.79], [12, 0.78], [12, 0.77], [12, 0.76],
/* size=12 */ [12, 1.00], [12, 0.97], [12, 0.96], [12, 0.95], [12, 0.93], [12, 0.92], [12, 0.91], [12, 0.90], [12, 0.89], [12, 0.87], [13, 0.82], [13, 0.81], [13, 0.80], [13, 0.79], [13, 0.78], [13, 0.77],
/* size=13 */ [13, 1.00], [13, 0.97], [13, 0.96], [13, 0.95], [13, 0.94], [13, 0.93], [13, 0.92], [13, 0.91], [13, 0.89], [13, 0.88], [14, 0.84], [14, 0.82], [14, 0.82], [14, 0.81], [14, 0.80], [14, 0.79],
/* size=14 */ [14, 1.00], [14, 0.98], [14, 0.96], [14, 0.95], [14, 0.94], [14, 0.93], [14, 0.92], [14, 0.91], [14, 0.90], [14, 0.89], [14, 0.88], [15, 0.84], [15, 0.82], [15, 0.82], [15, 0.81], [15, 0.80],
/* size=15 */ [15, 1.00], [15, 0.98], [15, 0.96], [15, 0.95], [15, 0.95], [15, 0.93], [15, 0.93], [15, 0.92], [15, 0.91], [15, 0.90], [15, 0.89], [16, 0.84], [16, 0.84], [16, 0.83], [16, 0.82], [16, 0.81],
];
```

### License

```
Copyright 2018 Yaroslav Serhieiev <noomorph@gmail.com>

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
