# What does it solve?

There is a transparent borderless *Button A* which is styled using `box-shadow` CSS property.
You have to create *Button B* which should look as similar as possible to *Button A* without using `box-shadow`.
Unfortunately, the only CSS properties you can use are either `border` or `outline`.

In our days it is common to search answers or ask smart people on *StackOverflow*, [StackOverflow](but sometimes nobody is interested or able to answer your question, like in my case).
Fortunately, I had some time and luck to conduct my own research and you came here in time, when I've got some useful results for you.

### Demo

<iframe id="demo-iframe" src="demo/index.html" width="100%" height="460" allowtransparency="true" frameborder="0" scrolling="no"></iframe>

### The Useful Code

```javascript
const SHADOW_APPROXIMATION_MAP = [
                  /*blur=00*/ /*blur=01*/ /*blur=02*/ /*blur=03*/ /*blur=04*/ /*blur=05*/ /*blur=06*/ /*blur=07*/ /*blur=08*/ /*blur=09*/ /*blur=10*/ /*blur=11*/ /*blur=12*/ /*blur=13*/ /*blur=14*/ /*blur=15*/
    /* size=00 */ [ 0, 0.00], [ 1, 0.20], [ 1, 0.27], [ 1, 0.33], [ 2, 0.25], [ 2, 0.28], [ 2, 0.31], [ 2, 0.33], [ 2, 0.33], [ 3, 0.30], [ 3, 0.30], [ 3, 0.31], [ 3, 0.31], [ 4, 0.29], [ 4, 0.30], [ 4, 0.30],
    /* size=01 */ [ 1, 1.00], [ 1, 0.79], [ 1, 0.71], [ 2, 0.48], [ 2, 0.48], [ 2, 0.48], [ 3, 0.39], [ 3, 0.40], [ 3, 0.40], [ 4, 0.35], [ 4, 0.35], [ 4, 0.36], [ 4, 0.36], [ 4, 0.37], [ 5, 0.34], [ 5, 0.34],
    /* size=02 */ [ 2, 1.00], [ 2, 0.88], [ 2, 0.81], [ 2, 0.76], [ 3, 0.59], [ 3, 0.58], [ 3, 0.56], [ 4, 0.47], [ 4, 0.47], [ 4, 0.47], [ 4, 0.47], [ 4, 0.47], [ 4, 0.47], [ 5, 0.42], [ 5, 0.42], [ 5, 0.42],
    /* size=03 */ [ 3, 1.00], [ 3, 0.92], [ 3, 0.87], [ 3, 0.83], [ 3, 0.79], [ 4, 0.66], [ 4, 0.64], [ 4, 0.62], [ 4, 0.62], [ 5, 0.52], [ 5, 0.52], [ 5, 0.52], [ 5, 0.52], [ 6, 0.46], [ 6, 0.45], [ 6, 0.45],
    /* size=04 */ [ 4, 1.00], [ 4, 0.94], [ 4, 0.90], [ 4, 0.87], [ 4, 0.84], [ 4, 0.81], [ 5, 0.69], [ 5, 0.67], [ 5, 0.67], [ 5, 0.64], [ 5, 0.64], [ 6, 0.56], [ 6, 0.56], [ 6, 0.55], [ 7, 0.49], [ 7, 0.49],
    /* size=05 */ [ 5, 1.00], [ 5, 0.95], [ 5, 0.92], [ 5, 0.89], [ 5, 0.87], [ 5, 0.85], [ 6, 0.74], [ 6, 0.72], [ 6, 0.72], [ 6, 0.68], [ 6, 0.68], [ 6, 0.66], [ 6, 0.66], [ 7, 0.58], [ 7, 0.58], [ 7, 0.58],
    /* size=06 */ [ 6, 1.00], [ 6, 0.96], [ 6, 0.93], [ 6, 0.91], [ 6, 0.89], [ 6, 0.87], [ 6, 0.84], [ 7, 0.75], [ 7, 0.75], [ 7, 0.71], [ 7, 0.71], [ 7, 0.70], [ 7, 0.70], [ 8, 0.62], [ 8, 0.61], [ 8, 0.61],
    /* size=07 */ [ 7, 1.00], [ 7, 0.96], [ 7, 0.94], [ 7, 0.92], [ 7, 0.90], [ 7, 0.89], [ 7, 0.86], [ 8, 0.78], [ 8, 0.78], [ 8, 0.75], [ 8, 0.75], [ 8, 0.73], [ 8, 0.73], [ 8, 0.70], [ 9, 0.64], [ 9, 0.64],
    /* size=08 */ [ 8, 1.00], [ 8, 0.96], [ 8, 0.95], [ 8, 0.93], [ 8, 0.91], [ 8, 0.90], [ 8, 0.88], [ 8, 0.86], [ 8, 0.86], [ 9, 0.77], [ 9, 0.77], [ 9, 0.75], [ 9, 0.75], [ 9, 0.72], [10, 0.67], [10, 0.67],
    /* size=09 */ [ 9, 1.00], [ 9, 0.97], [ 9, 0.95], [ 9, 0.94], [ 9, 0.92], [ 9, 0.91], [ 9, 0.89], [ 9, 0.87], [ 9, 0.87], [10, 0.79], [10, 0.79], [10, 0.77], [10, 0.77], [10, 0.75], [10, 0.73], [10, 0.73],
    /* size=10 */ [10, 1.00], [10, 0.97], [10, 0.96], [10, 0.94], [10, 0.93], [10, 0.92], [10, 0.90], [10, 0.89], [10, 0.89], [11, 0.80], [11, 0.80], [11, 0.79], [11, 0.79], [11, 0.76], [11, 0.75], [11, 0.75],
    /* size=11 */ [11, 1.00], [11, 0.98], [11, 0.96], [11, 0.95], [11, 0.93], [11, 0.92], [11, 0.91], [11, 0.89], [11, 0.89], [11, 0.86], [11, 0.86], [12, 0.81], [12, 0.81], [12, 0.78], [12, 0.77], [12, 0.77],
    /* size=12 */ [12, 1.00], [12, 0.98], [12, 0.96], [12, 0.95], [12, 0.94], [12, 0.93], [12, 0.91], [12, 0.90], [12, 0.90], [12, 0.87], [12, 0.87], [13, 0.82], [13, 0.82], [13, 0.80], [13, 0.78], [13, 0.78],
    /* size=13 */ [13, 1.00], [13, 0.98], [13, 0.97], [13, 0.95], [14, 0.91], [13, 0.94], [13, 0.93], [13, 0.91], [14, 0.87], [14, 0.86], [14, 0.84], [14, 0.83], [14, 0.83], [14, 0.82], [14, 0.80], [15, 0.77],
    /* size=14 */ [14, 1.00], [14, 0.98], [14, 0.97], [14, 0.96], [15, 0.92], [14, 0.95], [14, 0.93], [14, 0.91], [15, 0.88], [15, 0.87], [15, 0.85], [15, 0.84], [15, 0.84], [15, 0.83], [15, 0.81], [15, 0.82],
    /* size=15 */ [15, 1.00], [15, 0.98], [15, 0.97], [15, 0.96], [16, 0.92], [15, 0.95], [15, 0.93], [15, 0.92], [16, 0.89], [16, 0.87], [16, 0.86], [16, 0.84], [16, 0.85], [16, 0.84], [16, 0.82], [16, 0.83],
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
