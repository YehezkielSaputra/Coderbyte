# Coderbyte

## Table of Contents

| No. |  Questions                                   |
|-----|----------------------------------------------|
| 01. | [Bitmap Holes?](#bitmap-holes) |


## React Basics

01. ### Bitmap Holes
    Have the function BitmapHoles(strArr) take the array of strings stored in strArr, which will be a 2D matrix of 0 and 1’s, and determine how many holes, or contiguous regions of 0’s, exist in the matrix. A contiguous region is one where there is a connected group of 0’s going in one or more of four directions: up, down, left, or right. For example: if strArr is [“10111”, “10101”, “11101”, “11111”], then this looks like the following matrix:

1 0 1 1 1
1 0 1 0 1
1 1 1 0 1
1 1 1 1 1

For the input above, your program should return 2 because there are two separate contiguous regions of 0’s, which create “holes” in the matrix. You can assume the input will not be empty.

```javascript
    function BitmapHoles(strArr) {
    // declare an empty array to hold coordinates of all 0's
    var index = [],
        // initialize the number of holes to 0
        holes = 0,
        checker;
    // loop through each string in the array
    for (var i = 0; i < strArr.length; i++) {
        // split each string into individual characters
        strArr[i] = strArr[i].split('');
        // loop through each character
        for (var j = 0; j < strArr[i].length; j++) {
            // if the character is 0, add its coordinates to the index array
            if (strArr[i][j] === "0") {
                index.push([i, j]);
            }
        }
    }
    // loop through each coordinate in the index array
    for (var c = 0; c < index.length; c++) {
        checker = false;
        // loop through the remaining coordinates in the index array
        for (var k = c + 1; k < index.length; k++) {
            // if the two coordinates are adjacent, set the checker variable to true
            if (index[k][0] === index[c][0] + 1 && index[k][1] === index[c][1] || index[k][0] === index[c][0] && index[k][1] === index[c][1] + 1) {
                checker = true;
            }
        }
        // if the checker variable is still false, increment the holes variable
        if (checker === false) {
            holes += 1;
        }
    }
    // return the number of holes
    return holes;
}

// keep this function call here 
console.log(BitmapHoles(readline()));
```

<div align="right">
    <b><a href="#">back to top</a></b>
</div>
