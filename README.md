# Coderbyte

## Table of Contents

| No. |  Questions                                   |
|-----|----------------------------------------------|
| 01. | [Bitmap Holes](#bitmap-holes) |
| 02. | [Stock Picker](#stock-picker) |
| 03. | [Fibonacci Checker](#fibonacci-checker) |
| 04. | [Most Free Time](#most-free-time) |
| 05. | [Coin Determiner](#coin-determiner) |

## React Basics

01. ### Bitmap Holes
Have the function BitmapHoles(strArr) take the array of strings stored in strArr, which will be a 2D matrix of 0 and 1’s, and determine how many holes, or contiguous regions of 0’s, exist in the matrix. A contiguous region is one where there is a connected group of 0’s going in one or more of four directions: up, down, left, or right. For example: if strArr is [“10111”, “10101”, “11101”, “11111”], then this looks like the following matrix:

1 0 1 1 1 <br/>
1 0 1 0 1 <br/>
1 1 1 0 1 <br/>
1 1 1 1 1 <br/>

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
            if (index[k][0] === index[c][0] + 1 && index[k][1] === index[c][1] ||
                index[k][0] === index[c][0] && index[k][1] === index[c][1] + 1) {
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

02. ### Stock Picker
Have the function StockPicker(arr) take the array of numbers stored in arr which will contain integers that represent the amount in dollars that a single stock is worth, and return the maximum profit that could have been made by buying stock on day x and selling stock on day y where y > x. For example: if arr is [44, 30, 24, 32, 35, 30, 40, 38, 15] then your program should return 16 because at index 2 the stock was worth $24 and at index 6 the stock was then worth $40, so if you bought the stock at 24 and sold it at 40, you would have made a profit of $16, which is the maximum profit that could have been made with this list of stock prices.

If there is not profit that could have been made with the stock prices, then your program should return -1. For example: arr is [10, 9, 8, 2] then your program should return -1.

```javascript
    function StockPicker(arr) { 
    var profit=-1; // Initialize the maximum profit to -1
    var buyPrice=arr[0]; // Initialize the buying price to the first element of the array
    for(var i=1; i<arr.length; i++){ // Loop through the array starting from the second element
        if(arr[i]<buyPrice){ // If the current element is smaller than the buying price
            buyPrice=arr[i]; // Update the buying price
        }
        else if( (arr[i]-buyPrice) > profit){
            // If selling the stock at the current price will give a greater profit than the previous maximum profit
            profit=arr[i]-buyPrice; // Update the maximum profit
        }
    }
    
  return profit; // Return the maximum profit 
}
   
// keep this function call here 
console.log(StockPicker(readline()));
```

<div align="right">
    <b><a href="#">back to top</a></b>
</div>

03. ### Fibonacci Checker
Have the function FibonacciChecker(num) return the string yes if the number given is part of the Fibonacci sequence. This sequence is defined by: Fn = Fn-1 + Fn-2, which means to find Fn you add the previous two numbers up. The first two numbers are 0 and 1, then comes 1, 2, 3, 5 etc. If num is not in the Fibonacci sequence, return the string no.

```javascript
    function FibonacciChecker(num) {
    // Initialize an array with the first value of the Fibonacci sequence
    var prev = [0]
  
    // Loop through each number in the sequence up to and including the input number
      for (i = 1; i < num+1; i) {
        // Calculate the next number in the sequence by adding the previous two
        var check = i + prev[0]
    
    // If the calculated number is equal to the input number, return "yes"
    if (check === num) {
      return 'yes'
    }
    
    // Add the current number to the beginning of the array
    // to keep track of the previous two numbers
    prev.unshift(i)
    
    // Update the current number to be the next number in the sequence
    i = check
  }
  
  // If the input number is not in the Fibonacci sequence, return "no"
  return 'no' 
}
   
// keep this function call here 
console.log(FibonacciChecker(readline()));
```

<div align="right">
    <b><a href="#">back to top</a></b>
</div>

04. ### Most Free Time
Have the function MostFreeTime(strArr) read the strArr parameter being passed which will represent a full day and will be filled with events that span from time X to time Y in the day. The format of each event will be hh:mmAM/PM-hh:mmAM/PM. For example, strArr may be [“10:00AM-12:30PM”,”02:00PM-02:45PM”,”09:10AM-09:50AM”]. Your program will have to output the longest amount of free time available between the start of your first event and the end of your last event in the format: hh:mm. The start event should be the earliest event in the day and the latest event should be the latest event in the day. The output for the previous input would therefore be 01:30 (with the earliest event in the day starting at 09:10AM and the latest event ending at 02:45PM). The input will contain at least 3 events and the events may be out of order.

```javascript
    function MostFreeTime(strArr) { 
    // create an empty array to store the minutes of each event
    var minArr = []
    // create a variable to keep track of the longest free time
    var longest = 0
    
    // function to convert a time string to minutes
    function timeCalc(time) {
        var min = 0
        // add 12 hours (720 minutes) for pm times
        if(time.match(/pm/i)) {
            min += 720
        }
        // add the hours converted to minutes
        if(time.split(':')[0] !== '12') {
           min += time.split(':')[0] * 60
        } 
        // add the minutes
        min += Number(time.split(':')[1].match(/[0-9][0-9]/)[0])
        return min
    }
    
    // loop through the array of events and convert each time to minutes
    for(var i = 0; i < strArr.length; i++) {
        var time1 = strArr[i].split('-')[0]
        var time2 = strArr[i].split('-')[1]
        minArr.push([timeCalc(time1), timeCalc(time2)])
    }    
    
    // sort the array of minutes in ascending order
    minArr.sort(function(a, b) {
        return a[0] - b[0]
    })
    
    // loop through the sorted array and find the longest free time
    for(var j = 0; j < minArr.length - 1; j++) {
        if(longest < minArr[j + 1][0] - minArr[j][1]) {
            longest = minArr[j + 1][0] - minArr[j][1]
        }
    }
    
    // convert the longest free time to hours and minutes
    var hours = 0
    while(longest >= 60) {
        longest -= 60;
        hours ++
    }
    
    // add a leading zero if necessary for single-digit minutes and hours
    if(hours.toString().length === 1) {
        hours = "0" + hours
    }
    if(longest.toString().length === 1) {
        return hours + ":0" + longest
    } else {
        return hours + ":" + longest
    }
}

// keep this function call here 
console.log(MostFreeTime(readline()));
```

<div align="right">
    <b><a href="#">back to top</a></b>
</div>

05. ### Coin Determiner
Have the function CoinDeterminer(num) take the input, which will be an integer ranging from 1 to 250, and return an integer output that will specify the least number of coins, that when added, equal the input integer. Coins are based on a system as follows: there are coins representing the integers 1, 5, 7, 9, and 11. So for example: if num is 16, then the output should be 2 because you can achieve the number 16 with the coins 9 and 7. If num is 25, then the output should be 3 because you can achieve 25 with either 11, 9, and 5 coins or with 9, 9, and 7 coins.

```javascript
    function CoinDeterminer(num) { 
    //initialize count to 0
    var count = 0;
    
    //subtract 11 from num as many times as possible
    while(num>10){
        if(num % 11 > 1 && num % 11 < 5){
        // if the remainder of num divided by 11 is between 2 and 4,
        // subtract 9 instead of 11
            num -= 9; 
            count++; //increment count by 1
        } else {
            num -= 11; //subtract 11
            count++; //increment count by 1
        }
    }
    
    //subtract 9 from num as many times as possible
    while(num>8){
        if(num % 9 > 1 && num % 9 < 5){
        // if the remainder of num divided by 9 is between 2 and 4,
        // subtract 7 instead of 9
            num -= 7; 
            count++; //increment count by 1
        } else {
            num -= 9; //subtract 9
            count++; //increment count by 1
        }
    }
    
    //subtract 7 from num as many times as possible
    while(num>6){
        num -= 7; //subtract 7
        count++; //increment count by 1
    }
    
    //subtract 5 from num as many times as possible
    while(num>4){
        num -= 5; //subtract 5
        count++; //increment count by 1
    }
    
    //subtract 1 from num as many times as possible
    while(num>0){
        num -= 1; //subtract 1
        count++; //increment count by 1
    }
    
    //return the count
    return count;
}
// keep this function call here 
console.log(CoinDeterminer(readline()));
```

<div align="right">
    <b><a href="#">back to top</a></b>
</div>
