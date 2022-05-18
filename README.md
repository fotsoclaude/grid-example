# A layout using css grid

![Result](https://github.com/fotsoclaude/grid-example/blob/main/result.png)

## Usage of grid in CSS

### Using line numbers

```css
.container {
    /*initialization*/
    display: grid;

    /*Definition of x rows with the same size y*/
    grid-template-rows: repeat(x, y);

    /*Definition of 3 with size a, a, and b*/
    grid-template-rows: repeat(2, a) b;

    /*Definition of x rows with differents sizes*/
    grid-template-rows: a, b, c, ..., y;

    /*Definition of a gap for both columns and rows*/
    grid-gap: 30px;

    /*Definition of a different gap for both and rows*/
    grid-row-gap: 30px;
    grid-column-gap: 20px;
}
```

#### Spanning item
Disclaimer : Rows and columns are starting at 1
```css
.sidebar {
    /*The item start at the row 2 and end at 4, so it will extends on 2 rows*/
    grid-row: 2/4;
    /*
    The item start at the column 4 and end at 5. 
    This is added to avoid the position of the item at the beginning of the row
    */
    grid-column: 4/5;
}
```

### Using line names
```css
.container {
    /*initialization*/
    display: grid;

    grid-template-rows: [header-start] 100px 
                        [header-end boxes-start] 200px 
                        [box-end main-start] 400px
                        [main-end footer-start] 100px
                        [footer-end];


    /*
    When using repeat(), this will automatically create a nameset 
    "col-start 1" & "col-end 1" for the first,
    "col-start 2" & "col-end 2" for the seciond,
    "col-start 3" & "col-end 3" for the third 
    ...
    to avoid conflicting names
    */
    grid-template-columns: repeat(3, [col-start] 1fr [col-end]) 200px;
}

```

#### Spanning item
We can now use those name to position our items
```css
.sidebar {
    grid-row: boxes-start / main-end;
    grid-column: col-end 3/ grid-end;
}
```

### Using area name
```css
.container {
    /*initialization*/
    display: grid;

    grid-template-rows: 1fr 2fr 4fr 1fr;
    grid-template-columns: repeat(3, 1fr) 200px;

    /*
    We define an area template by positionning a reference or keyword according to the area position
    A string is a row and each keyword a coloumn

    To define an empty space in our layout we just place a dot as keyword

    Examples : 
    
    * The header is the four columns of the first row so we write its keyword 4 times in the first string which represents the first row
    
    * The sidebar is on the last column of both the 2nd and 3rd column, so we write its keyword twice at the end of both the 2nd and 3rd string.
    */

    grid-template-areas: "head head head head"
                         "box-1 box-2 box-3 side"
                         "main main main side"
                         "foot foot foot foot";
}

/*
On each element we add the property grid-area and give it the keyword according to the positon in our template
*/
.sidebar {
    grid-area: side;
}
```
### Align Grid items

```css
.conainer {
    /*Align items vertically*/
    align-items: center; /* stretch | center | end | start */
    /*Align items horizontally*/
    justify-items: center;
}

.item {
    /*Override the global state for this item in the grid*/
    align-self: start;
    justify-self: end;
}

```

### Align Tracks

```css
.conainer {
    /*Align tracks vertically*/
    align-content: center; /* space-around | space-between | space-evently | center | end | start */
    /*Align tracks horizontally*/
    justify-content: center;
}
```

### Manage extra content

In some case you can have a implicit grid due to the overlapping content. To automatically place it according to your design you can use 

```css
.container {
    /*Define the size of the extra content*/
    grid-auto-columns: .5fr;
    grid-auto-rows: 80px;

    /*
    Define the direction of the extra content either row or column 
    The keyword 'dense' is to avoid empty area which is the default behavior
    */
    grid-auto-flow: row dense; 
}
```