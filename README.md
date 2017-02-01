Color Bee
===================================

Generate your color palette into all of the files your team works with. Color Bee takes one JavaScript file of colors and creates .ase, .clr, .json, .scss, and .sketchpallete files. See how IBM uses this on [IBM Design Colors](https://www.github.com/ibm-design/colors).

## To Generate files

1. `yarn add color-bee` or `npm install color-bee`
3. Create `colors.js` like [our sample](/source/colors.js)
2. Create `index.js`:
```
var colorBee = require('color-bee');
colorBee({
  output: '' // Optional destination folder
  source: 'colors.js' // Optional file for your color palette
});
```
4. `node index.js`

## To Use Files

### For Apps

*To maintain color accuracy across applications, we recommend setting your computer's display color profile to sRGB. You can change this under system preferences/display/color.*

#### Adobe Illustrator

1. Download `.ase` file and open Adobe Illustrator
2. Select Window, then Swatches
3. In the Swatches Window, select the Swatches Library Menu
4. Select Other Libraries and then find the `.ase` file

#### Keynote

1. Download `.clr` file and open Keynote
2. Select the color wheel icon next to any color picker
3. In the Colors Window, select the Color Palettes Tab
4. Select the cog icon, then "Open" and find the `.clr` file

#### Sketch
There are two options for Sketch. One option uses the Colors Window for quick selection. The other option requires the Sketch Palettes Plugin, but allows you to quickly import the palette as global or document colors.

Colors Window Option

1. Download `.clr` file and open Sketch
2. Select View, then Show Colors
3. In the Colors Window, select the Color Palettes Tab
4. Select the cog icon, then "Open" and find the `.clr` file

Global/Document Colors Option

1. Install the [Sketch Palettes Plugin](https://github.com/andrewfiorillo/sketch-palettes) by following their instructions
2. Download `.sketchpalette` file and open Sketch
2. Select Plugins, then Sketch Palettes,
3. Decide if you want to add the palette to Global Colors or Document Colors
4. Select Load Palette, then find the `.sketchpalette` file

### For Development

#### Installation
The IBM Design Language Color Library can be installed via [npm](https://www.npmjs.com/).

npm
```bash
$ npm install ibm-design-colors --save
```

#### Sass

The .scss file will work with any Sass compiler compatible with Sass 3.3 or greater.

##### Color Palette

Returns the specified color from the specified color palette

###### `color($palette, [$grade: 'core'], $alpha)`

```scss
//////////////////////////////////////////////////
//  ------------------------------------------  //
// | Options       | Type          | Required | //
// |---------------|---------------|----------| //
// | Color Palette | String        | Yes      | //
// | Color grade    | String/Number | Optional | //
// | Color Alpha   | Number        | Optional | //
//  ------------------------------------------  //
//////////////////////////////////////////////////

background: color('blue', 80);     // #1d3649
background: color('blue');         // #4178be
-- with an alpha
background: color('blue', 80, $alpha: 0.5); // rgba(29, 54, 73, 0.5)
background: color('blue', $alpha: 0.5);     // rgba(65, 120, 190, 0.5)

```

##### Color Tint

Returns a color the specified amount of steps lighter than the given color in the given color's color palette

###### `color-tint($color, $amount)`

```scss
//////////////////////////////////////////////////
//  ------------------------------------------  //
// | Options       | Type          | Required | //
// |---------------|---------------|----------| //
// | Color Palette | Color         | Yes      | //
// | Tint Amount   | Number        | Yes      | //
//  ------------------------------------------  //
//////////////////////////////////////////////////

background: color-tint(color('blue', 80), 20);     // #325c80
background: color-tint(color('blue', 80), 23);     // #325c80
background: color-tint(color('blue', 80), 25);     // #4178be
background: color-tint(color('blue', 80), 100);    // #c0e6ff
```

##### Color Shade

Returns a color the specified amount of steps darker than the given color in the given color's color palette

###### `color-shade($color, $amount)`

```scss
//////////////////////////////////////////////////
//  ------------------------------------------  //
// | Options       | Type          | Required | //
// |---------------|---------------|----------| //
// | Color Palette | Color         | Yes      | //
// | Shade Amount  | Number        | Yes      | //
//  ------------------------------------------  //
//////////////////////////////////////////////////

background: color-shade(color('blue', 30), 20);     // #4178be
background: color-shade(color('blue', 30), 23);     // #4178be
background: color-shade(color('blue', 30), 25);     // #325c80
background: color-shade(color('blue', 30), 100);    // #010205
```

##### Get Colors

Returns the list of available color palettes if no parameter is passed in, all palettes and all of their colors if `'all'` is passed in, and all colors of a given palette if one is specified.

###### `get-colors([$palette])`

```scss
///////////////////////////////////////////
//  -----------------------------------  //
// | Options       | Type   | Required | //
// |---------------|--------|----------| //
// | Color Palette | String | Optional | //
//  -----------------------------------  //
///////////////////////////////////////////

$color-keys: get-colors();
$all-blues: get-colors('blue');
$full-color-map: get-colors('all');

//////////////////////////////
// Example Usage
//////////////////////////////

// Generating a class for each color palette
@each $color in $color-keys {
  .color--#{$color} {
    content: #{$color} is available;
  }
}

// Generate a class for each color of a color palette
@each $grade, $color in $all-blues {
  .blue--grade-#{$grade} {
    background: $color;
  }
}

// Generate a class for each color of each color palette
@each $palette-name, $palette in $full-color-map {
  @each $grade, $color in $palette {
    .#{$palette-name}--grade-#{$grade} {
      background: $color;
    }
  }
}
```

## To Contribute

### Setup

Setup the environment with [git](https://git-scm.com/) and [node](https://nodejs.org/en/) already installed. Then:

```bash
npm install yarn -g
git clone https://github.com/IBM-Design/color-bee.git
cd color-bee
yarn install
```

### Add file type

We love supporting different file types to cater to a variety of use cases. If you can add support to a new file type, please have it build from the source file when the `npm start` command is ran.
