# get

**get** string -> string

#### Definition

Get data from an internet resource. The argument is a string containing a URL. The result is a string that contains the information of the response. The purpose of this function is to pass the URLs of JSON objects to the 'data' function.

#### Examples

`get "my.url"`
> `{ "name": "William", "location": "Boulder" }`

`get "foo" "bar"`
> ERROR _Invalid URL._

#### Errors

1. _Invalid URL._
2. _Argument is not a valid string._

#### Tests

- [x] Test valid URL
- [x] Test invalid URL

---

# data

**data** string | record | list[record] -> object

#### Definition

Takes in a string specifying a JSON object, a record of the form {goal: num, value: num}, or a list thereof to specify the initial numeric data. All functions, unless otherwise stated, take 'data' or another function that acts on 'data' as a parameter. As such, it should typically be at the end of the expression.

#### Examples

`data {goal: 100, value: 50}`
> `{ "goal": [100], "value": [50], "progress": [50], ... }`

`data {"goal": 100, "notvalue": 50}`
> ERROR _Object missing parameters._

`data 2037`
> ERROR _Invalid parameters._

`data [{goal: 100, value: 50}, {goal: 200, value: 30}]`
> `{ "goal": [100, 200], "value": [50, 30], "progress": [50, 15], ... }`

#### Errors

1. _Object missing parameters._
2. _Invalid parameters._
3. _Object at index %i missing parameters._
4. _Object at index %i improperly formatted._

#### Tests

- [x] Test with goal and value
- [x] Test with only goal
- [x] Test with only value
- [x] Test with neither
- [x] Test with non-number goal/value
- [x] Test the above with first index of array
- [x] Test the above with multiple indices with the others correct
- [x] Test with above with multiple indices incorrect

---

# bar

**bar** object -> object

#### Definition

Sets the type of the graph to display as a bar graph or group of bar graphs. This also sets defaults for the graph size and thickness, if they have not been set already.

#### Examples

[`bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14049)

`bar {goal: 100}`
> ERROR _Argument Data invalid._

#### Errors

1. _Argument Data invalid._

#### Tests

- [x] Test with valid goal and value
- [x] Test with invalid goal and value

---

# radial

**radial** object -> object

#### Definition

Sets the type of the graph to display as a radial graph or group of concentric radial graphs. This also sets defaults for the graph size and thickness, if they have not been set already.

#### Examples

[`radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14051)

#### Errors

1. _Argument Data invalid._

#### Tests

- [x] Test with valid goal and value
- [x] Test with invalid goal and value

---

# size

**size** number object -> object

#### Definition

Takes in a positive number and sets the size of the graph specified. For bar graphs, this sets the length of the graph. For radial graphs, the size of the graph specifies the radius of the outermost graph, with the concentric graphs inside of that area.

#### Examples

[`size 100 radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14053)

`size "-30" radial data {goal: 100, value: 50}`
> ERROR _Argument must be a positive number._

#### Errors

1. _Argument Data invalid._
2. _Argument must be a positive number._

#### Tests

- [x] Test range of sizes
- [x] size 100
- [x] size "-30"
- [x] size 1000
- [x] size 0

---

# thickness

**thickness** number object -> object

#### Definition

Takes in a positive number and sets the width of the graph specified. The thickness of each bar is equal, and is determined by this value.

#### Examples

[`thickness 20 bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14054)

[`thickness 20 radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14056)

#### Errors

1. _Argument Data invalid._
2. _Argument must be a positive number._

#### Tests

- [x] Test range of thicknesses
- [x] thickness 10
- [x] thickness "-30"
- [x] thickness 1000
- [x] thickness 0

---

# inner-radius

**inner-radius** number object -> object

#### Definition

Takes in a positive number less than the previously specified graph size, and specifies the radius of the innermost graph in radial graphs. This sets the thickness based on the number of graphs to satisfy the desired value.

#### Examples

[`inner-radius 20 radial data [{goal: 100, value: 50}, {goal: 200, value: 30}]`](http://www.graffiticode.com/item?id=14081)

#### Errors

1. _Argument Data invalid._
2. _Argument must be a positive number._
3. _Inner radius must be less than outer._

#### Tests

- [x] Test range of inner-radii
- [x] inner-radius 10
- [x] inner-radius "-30"
- [x] inner-radius 1000
- [x] inner-radius 0

---

# gap

**gap** number object -> object

#### Definition

Takes in a positive number and specifies the distance between graphs in both bar and radial graphs. In bar graphs, this defaults to a five pixel buffer. In radial graphs, this defaults to the thickness of the graph.

#### Examples

[`gap 20 radial data [{goal: 100, value: 50}, {goal: 200, value: 30}]`](http://www.graffiticode.com/item?id=14089)

[`gap 25 inner-radius 20 radial data [{goal: 100, value: 50}, {goal: 200, value: 30}]`](http://www.graffiticode.com/item?id=14099)

[`gap 20 bar data [{goal: 100, value: 50}, {goal: 200, value: 30}]`](http://www.graffiticode.com/item?id=14108)

#### Errors

1. _Argument Data invalid._
2. _Argument must be a positive number._

#### Tests

- [ ] Test range of gaps
- [x] gap 10
- [x] gap "-30"
- [ ] gap 1000
- [x] gap 0

---

# dividers

**dividers** number object -> object

#### Definition

Takes in a positive number and displays the graph with the specified number of dividers. The last divider is transparent based on the progress remaining.

#### Examples

[`dividers 12 radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14112)

[`dividers 12 bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14115)

#### Errors

1. _Argument Data invalid._
2. _Argument must be a positive number._

#### Tests

- [ ] Test range of dividers
- [x] dividers 10
- [x] dividers "-30"
- [ ] dividers 1000
- [x] dividers 0

---

# divider-width

**divider-width** number object -> object

#### Definition

Takes in a positive number and sets the width of the space between dividers accordingly. This fails if the space is too wide for the dividers themselves to fit.

#### Examples

[`divider-width 10 dividers 12 radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14117)

[`divider-width 25 dividers 12 radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14119)

`divider-width 30 dividers 12 radial data {goal: 100, value: 50}`
> ERROR _Dividers too large to fit._

#### Errors

1. _Argument Data invalid._
2. _Argument must be a positive number._
3. _Dividers too large to fit._

#### Tests

- [x] Test range of divider-widths
- [x] divider-width 10
- [x] divider-width "-30"
- [x] divider-width 1000
- [x] divider-width 0

---

# arc

**arc** number object -> object

#### Definition

Takes in a positive number less than 360 and sets the fraction of the specified radial graph, in degrees, to display.

#### Examples

[`arc 180 radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14124)

#### Errors

1. _Argument Data invalid._
2. _Argument must be a positive number._
3. _Argument must be between 0 and 360._

#### Tests

- [x] Test range of arcs
- [x] arc 30
- [x] arc "-30"
- [x] arc 370
- [x] arc 0

---

# rotate

**rotate** number object -> object

#### Definition

Takes in a number in degrees and rotates the specified graph by the same amount. Unlike arc, this supports any number.

#### Examples

[`rotate 90 radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14126)

[`rotate 90 bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14127)

#### Errors

1. _Argument Data invalid._
2. _Argument must be a number._

#### Tests

- [x] Test range of rotations
- [x] rotate 30
- [x] rotate "-30"
- [x] rotate 370
- [x] rotate 0
- [x] rotate 1000

---

# animate

**animate** number object -> object

#### Definition

Takes in a positive number and sets the specified graph to fill itself in - that is, increase in value to the specified amount - during the given number of seconds. This defaults to zero, resulting in no animation occurring.

#### Examples

[`animate 3 radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14128)

[`animate 3 bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14129)

[`animate 3 dividers 12 bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14130)

#### Errors

1. _Argument Data invalid._
2. _Argument must be a positive number._

#### Tests

- [x] Test range of lengths
- [x] animate 3
- [x] animate "-30"
- [x] animate 0
- [x] animate 1000

---

# secondary-bar

**secondary-bar** object -> object

#### Definition

Sets the specified radial graph to create a secondary, inner bar that displays the remainder of the value given, provided it is over 100%.

#### Examples

[`secondary-bar radial data {goal: 100, value: 120}`](http://www.graffiticode.com/item?id=14131)

#### Errors

1. _Argument Data invalid._

---

# rounding

**rounding** number object -> object

#### Definition

Takes in a positive number and sets the specified graph to have edges rounded with the given radius.

#### Examples

[`rounding 5 bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14132)

[`rounding 5 thickness 10 radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=22590)

#### Errors

1. _Argument Data invalid._
2. _Argument must be a positive number._

#### Tests

- [x] Test range of roundings
- [x] rounding 0
- [x] rounding 3
- [x] rounding "-3"
- [x] rounding 30
- [x] rounding 100

---

# labels

**labels** string object -> object

#### Definition

Takes in a string and sets the specified graph to have labels numerically displaying progress. In the case of bar graphs, the string need only be set to "on". In radial graphs, the string can specify the position of the labels relative to the graph with strings such as "top left", "middle right", or "bottom center". Labels use the same number of decimal places as the initial values given in 'data', though this caps at 4 decimal places. If the string parameter starts with 'key', the label also has a color key for the fill colors of the graphs.

#### Examples

[`labels "on" bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14133)

[`labels "top right" radial data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14136)

[`labels "bottom middle" radial data {goal: 200, value: "33.33"}`](http://www.graffiticode.com/item?id=14139)

#### Errors

1. _Argument Data invalid._
2. _Invalid label option. Please try a direction such as 'top left'._

#### Tests

- [x] Test all label positions
- [x] Test with invalid label position

---

# fraction

**fraction** object -> object

#### Definition

Sets the specified, labelled graph to display progress in the form of the fraction of progress over goal rather than a percentage.

#### Examples

[`fraction labels "on" bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14140)

#### Errors

1. _Argument Data invalid._

---

# style

**style** record object -> object

#### Definition

Takes in an object with CSS style parameters and formats the labels of the specified graph accordingly. Use at own risk.

#### Examples

[`style {font-family: 'trebuchet ms', fill: '#0f0'} labels "on" bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14146)

#### Errors

1. _Argument Data invalid._

---

# text

**text** string | list[string] object -> object

#### Definition

Takes in a string or list thereof and uses it for the labels in the specified graph. This function allows %percent, %fraction, %goal, and %value to be replaced with animation-friendly values within the string. The list must be at least as long as the number of values in the data.

#### Examples

[`bar text "Goal is %goal, current is %value." animate 1 labels "bottom" data {goal: 100, value: 85}`](http://www.graffiticode.com/item?id=14316)

#### Errors

1. _Argument Data invalid._
2. _Argument array is too small for the data._
3. _Argument is not a string or array thereof._
4. _Index %i is not a string._

#### Tests

- [x] Test all keywords
- [x] Test array of insufficient size
- [x] Test oversized array
- [x] Test non-string
- [x] Test with keyword at the end of string
- [x] Test with keyword at the beginning of string

---

# image

**image** string number number string object -> object

#### Definition

Takes in a string specifying position (see label), a height, a width, and a url for an image, which is placed on the graph at the desired position.

#### Examples

[`image "center" 60 60 "http://artcompiler.com/logo.png" radial data {goal: 100, value: 85}`](http://www.graffiticode.com/item?id=14755)

#### Errors

1. _Argument Data invalid._
2. _Invalid URL._
3. _Argument must be a positive number._
4. _Invalid position option. Please try a direction such as 'top left'._

#### Tests

- [x] Test valid URL
- [ ] Test invalid URL
- [x] Test all position options
- [x] Test range of sizes

---

# rgba

**rgba** number number number number -> object

#### Definition

Takes in four positive numbers, the first three below 255, and outputs a color and opacity to be used by the color specification functions. This does not require a specified graph, and is typically passed in as a parameter to the aforementioned functions.

#### Examples

`rgba 255 0 0 50`
> `{ "r": 255, "g": 0, "b": 0, "a": 0.5 }`

#### Errors

1. _Argument must be between 0 and 255._
2. _Alpha must be a positive number._

#### Tests

- [x] Test range of values
- [x] r/g/b 0
- [x] r/g/b 100
- [x] r/g/b 260
- [x] r/g/b "-100"
- [x] a 0
- [x] a 10
- [x] a 100
- [x] a "-10"

---

# brewer

**brewer** number string object -> list[string]

#### Definition

Takes in a positive number and a string specifying a brewer palette and outputs a list of colors to be used by the color specification functions. The terminology takes a color or set of colors, such as "yellow green" or "orange red". This does not require a specified graph, and is typically passed in as a parameter to the aforementioned functions.

#### Examples

`brewer 4 "green"`
> `["#edf8e9","#bae4b3","#74c476","#238b45"]`

### Brewer Color Options
* yellow green
* yellow green blue
* green blue
* blue green
* purple blue green
* purple blue
* blue purple
* red purple
* purple red
* orange red
* yellow orange red
* yellow orange brown
* purple
* blue
* green
* orange
* red
* grey
* purple orange
* brown bluegreen
* purple green
* pink yellowgreen
* red blue
* red grey
* red yellow blue
* red yellow green
* spectral
* dark
* pastel
* accent

#### Errors

1. _Unrecognized color._
2. _Invalid size parameter._

#### Tests

- [x] Test all options
- [x] Test with invalid keyword
- [x] brewer 0
- [x] brewer 5
- [x] brewer 20

---

# fill

**fill** list[object] | list[string] object -> object

#### Definition

Takes in a list of colors and sets the bar color of the specified graph. In the case of a group of graphs, the list of colors is used in order before looping back to the start if there are less colors than graphs.

#### Examples

[`fill [rgb 255 0 0] bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14148)

[`fill [rgba 255 0 0 50] bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14149)

[`fill brewer 4 "green" bar data [{goal: 100, value: 50}, {goal: 200, value: 30}, {goal: 200, value: "33.33"}, {goal: 100, value: 79}]`](http://www.graffiticode.com/item?id=14153)

#### Errors

1. _Argument Data invalid._
2. _Please provide an array or brewer color._
3. _Index %i is not a valid hex string or rgb color._

#### Tests

- [x] fill with correct rgb color
- [x] fill with correct rgba color
- [x] fill with correct brewer color
- [x] fill with correct rgb color array
- [x] fill with correct rgba color array
- [x] fill with correct mixed color array
- [x] fill with incorrect versions of the above
- [x] fill with mixed versions of the above

---

# bar-background

**bar_background** list[object] | list[string] object -> object

#### Definition

Takes in a color or list of colors and sets the background bar color of the specified graph. In the case of a group of graphs, the list of colors is used in order before looping back to the start if there are less colors than graphs.

#### Examples

[`bar-background [rgb 255 0 0] bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14154)

[`bar-background [rgba 255 0 0 50] bar data {goal: 100, value: 50}`](http://www.graffiticode.com/item?id=14155)

[`bar-background brewer 4 "red" bar data [{goal: 100, value: 50}, {goal: 200, value: 30}, {goal: 200, value: "33.33"}, {goal: 100, value: 79}]`](http://www.graffiticode.com/item?id=14156)

#### Errors

1. _Argument Data invalid._
2. _Please provide an array or brewer color._
3. _Index %i is not a valid hex string or rgb color._

#### Tests

- [x] fill with correct rgb color
- [x] fill with correct rgba color
- [x] fill with correct brewer color
- [x] fill with correct rgb color array
- [x] fill with correct rgba color array
- [x] fill with correct mixed color array
- [x] fill with incorrect versions of the above
- [x] fill with mixed versions of the above

---

# opacity

**opacity** number object -> object

#### Definition

Takes in a positive number and sets the bar opacity of the specified graph. This is used as the default opacity for all graphs that do not have a specified alpha on their colors.

#### Examples

[`opacity 50 fill brewer 4 "red" bar data [{goal: 100, value: 50}, {goal: 200, value: 30}, {goal: 200, value: "33.33"}, {goal: 100, value: 79}]`](http://www.graffiticode.com/item?id=14157)

#### Errors

1. _Argument Data invalid._
2. _Alpha must be a positive number._

#### Tests

- [x] test range of opacities
- [x] opacity 0
- [x] opacity 10
- [x] opacity 100
- [x] opacity "-10"

---

# backopacity

**backopacity** number object -> object

#### Definition

Takes in a positive number and sets the background bar opacity of the specified graph. This is used as the default opacity for all graphs that do not have a specified alpha on their background colors.

#### Examples

[`backopacity 50 bar-background brewer 4 "red" bar data [{goal: 100, value: 50}, {goal: 200, value: 30}, {goal: 200, value: "33.33"}, {goal: 100, value: 79}]`](http://www.graffiticode.com/item?id=14162)

#### Errors

1. _Argument Data invalid._
2. _Alpha must be a positive number._

#### Tests

- [x] test range of opacities
- [x] backopacity 0
- [x] backopacity 10
- [x] backopacity 100
- [x] backopacity "-10"

---

# background

**background** number -> null

#### Definition

Takes in a positive number and sets the background bar opacity of the specified graph. This is used as the default opacity for all graphs that do not have a specified alpha on their background colors.

#### Examples

[`background rgb 50 50 50`](http://www.graffiticode.com/item?id=14184)

#### Errors

1. _Argument Data invalid._
2. _Argument is not a valid color._

#### Tests

- [x] fill with correct rgb color
- [x] fill with correct rgba color
- [x] fill with invalid object
