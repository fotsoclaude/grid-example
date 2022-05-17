# A layout using css grid

![Résultat](https://github.com/fotsoclaude/grid-example/blob/main/result.png)

## Usage of grid in CSS

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

### Spanning item
Disclaimer : Rows and columns are starting at 1
```css
.sidebar {
    /*The item start at the row 2 and end at 4, so it will extends on 2 rows*/
    grid-row: 2/4;ç
    /*The item start at the column 4 and end at 5. This is added to avoid the position of the item at the beginning of the row*/
    grid-column: 4/5;
}
```