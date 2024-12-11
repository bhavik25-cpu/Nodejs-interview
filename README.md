# javascript-interview-coding

https://codesandbox.io/p/devbox/express-js-forked-rfn7q9

https://github.com/lydiahallie/javascript-questions

1 Call back code 
 ```javascript
function doSomethingAsync(callback) {
  console.log("Doing something asynchronously...");
  
  // Simulate an asynchronous operation, like fetching data from a server
  setTimeout(() => {
    console.log("Operation completed!");
    
    // Invoke the callback function
    callback();
  }, 2000);
}

// Callback function to be passed
function callbackFunction() {
  console.log("Callback function executed!");
}

// Call the main function with the callback
doSomethingAsync(callbackFunction);
```

____________________________________________________________________________________________________________________________


Provide an example of closure in JavaScript.
```javascript

function outerFunction() {
  let outerVariable = "I am from the outer function";

  function innerFunction() {
    console.log(outerVariable);
  }

  return innerFunction;
}

// Create a closure by calling outerFunction and assigning the result to a variable
let closureExample = outerFunction();

// Call the inner function, which still has access to outerVariable
closureExample();
 // Output: "I am from the outer function"
```

_________________________________________________________________________________

2  promises
 ```javascript
// Function that returns a promise
function asyncFunction(value) {
  return new Promise((resolve, reject) => {
    // Simulating an asynchronous operation (e.g., reading from a database or making an API call)
    setTimeout(() => {
      if (value) {
        resolve(`Success: ${value}`);
      } else {
        reject('Error: Value is undefined');
      }
    }, 1000); // Simulating a delay of 1 second
  });
}

// Using the promise
asyncFunction('Hello')
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.error(error);
  })
  .finally(() => {
    console.log('Promise completed');
  });

 ```


___________________________________________________________________________

Promise.all

 ```javascript


const fetchData = async () => {
  try {
    const apiUrls = [
      'https://api.example.com/endpoint1',
      'https://api.example.com/endpoint2',
      'https://api.example.com/endpoint3'
    ];

    // Map over the URLs and create an array of fetch promises
    const requests = apiUrls.map((url) => fetch(url));

    // Use Promise.all to resolve all promises concurrently
    const responses = await Promise.all(requests);

    // Check for errors in responses and process the data
    const dataPromises = responses.map((response) => {
      if (!response.ok) {
        throw new Error(`Failed to fetch from ${response.url}`);
      }
      return response.json();
    });

    // Resolve data promises to get the final data
    const data = await Promise.all(dataPromises);

    console.log(data); // Logs an array of resolved API data
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};

fetchData();
 ```

________________________________________________________________________________________________________________________________________



asynchronous code


```javascript

// Function that returns a Promise to simulate an asynchronous operation
function fetchData() {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log("Data fetched successfully!");
      resolve("Fetched Data");
    }, 2000);
  });
}

// Asynchronous function using async/await
async function fetchDataAsync() {
  console.log("Fetching data asynchronously...");

  try {
    // Use await to wait for the Promise to resolve
    const data = await fetchData();
    console.log("Received data:", data);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}

// Call the asynchronous function
fetchDataAsync();
```

__________________________________________________________________________________________________________________________________________________________

How To find duplicate elements in array in javascript|

```javascript

// Function to find duplicate elements in an array
function findDuplicates(arr) {
  // Array to store the found duplicate elements
  var duplicates = [];

  // Loop through each element in the array
  for (var i = 0; i < arr.length - 1; i++) {
    // Nested loop to compare the current element with the rest of the elements
    for (var j = i + 1; j < arr.length; j++) {
      // Check if the elements are equal and the element is not already in the duplicates array
      if (arr[i] === arr[j] && !duplicates.includes(arr[i])) {
        // If true, add the duplicate element to the duplicates array
        duplicates.push(arr[i]);
      }
    }
  }

  // Return the array containing duplicate elements
  return duplicates;
}

// Example array
var myArray = [1, 2, 3, 4, 2, 5, 6, 3, 7, 8, 9, 4];
// Call the function to find duplicate elements
var duplicateElements = findDuplicates(myArray);
// Print the result to the console
console.log("Duplicate elements: ", duplicateElements);
```
__________________________________________________________________________________________________________________________________________________

hosting
```javascript

fun();

function fun() {
  console.log("x");  x
}

fun(); // This would result in an error

const fun = function() {
  console.log("x");
};
```
______________________________________________________________________________________________________________________

```javascript

const nestedArray = [1, [2, 3], [4, [5, 6]]];
const flattenedArray = nestedArray.flat(2);
console.log(flattenedArray); 
```
op : [ 1, 2, 3, 4, 5, 6 ]

_____________________________________________________________________________________________________________________

without any inbuild method
```javascript
function flattenArray(arr) {
  let result = [];

  for (let i = 0; i < arr.length; i++) {
    if (Array.isArray(arr[i])) {
      // Recursively flatten nested arrays
      result = result.concat(flattenArray(arr[i]));
    } else {
      result.push(arr[i]);
    }
  }

  return result;
}

const arr = [1, 2, [3, 4], 5, [6, 7], 8];
const output = flattenArray(arr);
console.log(output)
```
_____________________________________________________________________________________
```javascript

function flatArray(arr) {
    const result = [];

    function flatten(input) {
        for (let i = 0; i < input.length; i++) {
            if (Array.isArray(input[i])) {
                flatten(input[i]);
            } else {
                result.push(input[i]);
            }
        }
    }

    flatten(arr);
    return result;
}

const arr = [1, 2, [3, 4], 5, [6, 7], 8];
console.log(flatArray(arr)); // Output: [1, 2, 3, 4, 5, 6, 7, 8]
```

__________________________________________________________________________


let arr = [1,2,4,[2,4,[67,7]]]
output = [1,2, 4, 2,4,67,7]
```javascript
function flattenArray(arr) {
    let result = [];

    for (let i = 0; i < arr.length; i++) {
        if (typeof arr[i] === 'object' && arr[i] !== null) {
            // If it's an array, call flattenArray recursively
            let flattenedSubArray = flattenArray(arr[i]);
            for (let j = 0; j < flattenedSubArray.length; j++) {
                result[result.length] = flattenedSubArray[j];  // Directly set the value in the result array
            }
        } else {
            // If it's not an array, directly push the value to the result array
            result[result.length] = arr[i];
        }
    }

    return result;
}

// Example usage:
let arr = [1, 2, 4, [2, 4, [67, 7]]];
let flattened = flattenArray(arr);
console.log(flattened);  // Output: [1, 2, 4, 2, 4, 67, 7]



```


_______________________________________________________________________

flat

```javascript

function mynewarr(arr){
    return arr.reduce((one , two) => 
        Array.isArray(two) ? one.concat(mynewarr(two)) : one.concat(two)
    ,[])
    
}

const arr = [1,[2,[3,4],5]]
const result = mynewarr(arr)
console.log(result)

```

[ 1, 2, 3, 4, 5 ]

______________________________________________________________________________________________________________________
```javascript

const arr = [1, 2, 3, 4];
const rotatedArr = arr.slice(2).concat(arr.slice(0, 2));
console.log(rotatedArr);op: [ 3, 4, 1, 2 ]
```
______________________________________________________________________________________________________________________
without inbuild function
```javascript
const arr = [1, 2, 3, 4];
const rotations = 2; // Number of rotation
for (let i = 0; i < rotations; i++) {
  const firstElement = arr[0];
  for (let j = 1; j < arr.length; j++) {
    arr[j - 1] = arr[j];
  }
  arr[arr.length - 1] = firstElement;
}
console.log(arr); // Output: [3, 4, 1, 2]
```

______________________________________________________________________________________________________________________
```javascript
const a = [1,2,3,4]
const b = a;
a[0] = 8;
console.log('a is : ', a);
console.log('b is : ', b)
```
op:
a is :  [ 8, 2, 3, 4 ]
b is :  [ 8, 2, 3, 4 ]
______________________________________________________________________________________________________________________
```javascript

var a = [1,2,3,4]
var b = a;
a = [7,8]
console.log(a);
console.log(b)
```
op
[ 7, 8 ]
[ 1, 2, 3, 4 ]
___________________________________________________________________________________________________________________________________________________________


You are given a string S and its length n and you need to sort its characters based on their frequency. The characters in the output will be ordered based on their frequency in S, characters with higher frequency come first.

For example,

Input: S = "halalelluejah"

Output: llllaaahheeuj

Input: S = "aaaabeebccccc"

Output: cccccaaaabbee

```javascript

const sortCharsByFrequency = str => {
  const charCount = {};
  
  // Count character frequencies
  for (const char of str) {
    charCount[char] = (charCount[char] || 0) + 1;
  }

  // Sort characters based on frequency
  const sortedChars = Object.keys(charCount).sort((a, b) => charCount[b] - charCount[a]);

  // Generate the result string
  const result = sortedChars.map(char => char.repeat(charCount[char])).join('');

  return result;
};

// Test cases
const input1 = "halalelluejah";
const input2 = "aaaabeebccccc";

console.log(sortCharsByFrequency(input1)); // Output: llllaaahheeuj
console.log(sortCharsByFrequency(input2)); // Output: cccccaaaabbee
```
____________________________________________________________________________________________________________________________________________________

Input:  { 3, 4, -7, 3, 1, 3, 1, -4, -2, -2 }

Output: Subarray with zero-sum exists

The subarrays with a sum of 0 are:

{ 3, 4, -7 }, { 4, -7, 3 }, { -7, 3, 1, 3 }, { 3, 1, -4 }, { 3, 1, 3, 1, -4, -2, -2 }, { 3, 4, -7, 3, 1, 3, 1, -4, -2, -2 }
```javascript

const hasZeroSumSubarray = arr => {
  const set = new Set();
  let sum = 0;

  return arr.some(element => {
    sum += element;
    if (set.has(sum) || sum === 0) {
      return true;
    }
    set.add(sum);
    return false;
  });
};

const inputArray = [3, 4, -7, 3, 1, 3, 1, -4, -2, -2];

if (hasZeroSumSubarray(inputArray)) {
  console.log("Subarray with zero-sum exists");
} else {
  console.log("Subarray with zero-sum does not exist");
}


```
____________________________________________________________________________________________________________________________________________________

0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1 do in ascending order in js use sort method

output  0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 20

To sort the array [0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1] in ascending order in JavaScript using the sort method, you can use the following

```javascript

var array = [0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1];
// Use the sort method with a custom comparator function
array.sort(function(a, b) {
  return a - b;
});
console.log(array);
```
_________________________________________________________________________________________________________________________________________________________

without any inbuild method
```javascript

function bubbleSort(arr) {
    var len = arr.length;
    for (var i = 0; i < len; i++) {
        for (var j = 0; j < len - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                var temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    return arr;
}

var array = [0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1];
console.log("Before sorting:", array);
console.log("After sorting:", bubbleSort(array));
```

op: [  0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2]

_____________________________________________________________________________________________________________________________________
```javascript

function func2(){

  for(var i = 0; i < 3; i++){

    setTimeout(()=> console.log(i),2000);

}

}

func2();
```

OP:

3
3
3

_____________________________________________________________________________________________
```javascript

const a = "india is my country";
// Function to capitalize the first letter of each word
function capitalizeWords(str) {
    return str.split(' ').map(word => word.charAt(0).toUpperCase() + word.slice(1)).join('');
}
// Capitalize words and remove spaces
const result = capitalizeWords(a).replace(/\s/g, '');
// Display the result
console.log(result);
```

OP: IndiaIsMyCountry
_____________________________________________________________________________________
```javascript

const a = "india is my country";

function capitalizeWordsAndRemoveSpaces(str) {
    let result = '';
    let capitalizeNext = true;

    for (let i = 0; i < str.length; i++) {
        if (str[i] === ' ') {
            capitalizeNext = true;
        } else {
            if (capitalizeNext) {
                result += str[i].toUpperCase();
                capitalizeNext = false;
            } else {
                result += str[i];
            }
        }
    }

    return result;
}

const result = capitalizeWordsAndRemoveSpaces(a);
console.log(result);

```

______________________________________________________________________________________

How to find the second largest element in an array
```javascript

function findSecondLargest(arr) {
  // Sort the array in descending order
  arr.sort(function(a, b) {
    return b - a;
  });

  // The second element in the sorted array is the second largest
  return arr[1];
}

// Example usage:
const myArray = [10, 5, 8, 20, 3];
const secondLargest = findSecondLargest(myArray);

console.log("Second Largest Element:", secondLargest);

```
__________________________________________________________________________________________________________________________________
without inbuild method
```javascript

function findSecondLargest(arr) {
  let largest = -Infinity;
  let secondLargest = -Infinity;

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] > largest) {
      secondLargest = largest;
      largest = arr[i];
    } else if (arr[i] > secondLargest && arr[i] !== largest) {
      secondLargest = arr[i];
    }
  }

  return secondLargest !== -Infinity ? secondLargest : null;
}

// Example usage:
const myArray = [10, 5, 8, 20, 3];
const secondLargest = findSecondLargest(myArray);

console.log("Second Largest Element:", secondLargest);

```
_________________________________________________________________________________________________________________________________________________________________________

Find the Largest & Smallest Elem in an Array in JavaScript
```javascript

function findLargest(arr) {
  const max = Math.max(...arr);
  const min = Math.min(...arr);
  return{
      max , min
  }

}

// Example usage:
const myArray = [10, 5, 8, 20, 3];
const {max,min} = findLargest(myArray);

console.log("Largest Element:", max);
console.log("Largest Element:", min);
```

op:

Largest Element: 20
Largest Element: 3
__________________________________________________________________________________________________________________________
```javascript

function findLargest(arr) {
  if (arr.length === 0) {
    return "Array is empty";
  }

  let max = arr[0];
  let min = arr[0];

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i];
    }
    if (arr[i] < min) {
      min = arr[i];
    }
  }

  return { max, min };
}

// Example usage:
const myArray = [10, 5, 8, 20, 3];
const { max, min } = findLargest(myArray);

console.log("Largest Element:", max);
console.log("Smallest Element:", min);
```
Op
function findLargest(arr) {
  if (arr.length === 0) {
    return "Array is empty";
  }

  let max = arr[0];
  let min = arr[0];

  for (let i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
      max = arr[i];
    }
    if (arr[i] < min) {
      min = arr[i];
    }
  }

  return { max, min };
}

// Example usage:
const myArray = [10, 5, 8, 20, 3];
const { max, min } = findLargest(myArray);

console.log("Largest Element:", max);
console.log("Smallest Element:", min);


_____________________________________________________________________________________________________________________________________________________
```javascript

const person = {
  name: 'Lydia',
  age: 21,
};

for (const item in person) {
  console.log(item);
}
```

op: 
name
age
______________________________________________________________________________________________________________________________________________________
```javascript

let a = "25"
let b = 25
console.log(a == b);
console.log( 99 + 1 + "10")
```

op:
true
10010

___________________________________________________________________________________________________________________________________________
```javascript

setTimeout(function() {
     console.log('First Line');
}, 0);

console.log('Second Line');
console.log('Third Line');
```

op:
Second Line
Third Line
First Line

______________________________________________________________________________________________________________________________________________
```javascript

function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}
const lydia = new Person('Lydia', 'Hallie');
const sarah = Person('Sarah', 'Smith');
console.log(lydia.name);
console.log(sarah.name);
```

op:
console.log(sarah.lastName
TypeError: Cannot read properties of undefined (reading 'lastName')


_____________________________________________________________________________________________________________________________
```javascript

function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const lydia = new Person('Lydia', 'Hallie');
const sarah = new Person('Sarah', 'Smith'); // Use 'new' here
console.log(lydia.firstName); 
console.log(sarah.lastName);
```

op:
Lydia
Smith
_______________________________________________________________________________________________________________________________
```javascript

const user = {
    name: 'Raj',
    location: {
        city: 'NY',
        state: 'NY'
    }
};
user.location.zipcode=401107
console.log(user)
```

op:
{ name: 'Raj', location: { city: 'NY', state: 'NY', zipcode: 401107 } }

-------------------------------------------------------------------------------------------------------------
```javascript

const c = [1,2,3,4,5];
c = [...c, 6]
console.log(c)
```

op:

TypeError: Assignment to constant variable.
use let and var
__________________________________________________________________________________________________________
```javascript

let a = 12;
--a;
console.log(a++);
console.log(a)
```

op:
11
12

______________________________________________________________________________________________________

Look at this series: 12, 11, 13, 12, 14, 13, 15,...
```javascript

function generateSeries(n) {
  const series = [12];
  for (let i = 1; i < n; i++) {
    if (i % 2 === 1) {
      // If the index is odd, subtract 1
      series.push(series[i - 1] - 1);
    } else {
      // If the index is even, add 2
      series.push(series[i - 1] + 2);
    }
  }
  return series;
}

const n = 10; // You can change this value to generate more or fewer terms
const result = generateSeries(n);
console.log(result);
```

op:
[
  12, 11, 13, 12, 14,
  13, 15, 14, 16, 15
]

__________________________________________________________________________________________________________________________________________
with inbuild function
```javascript

const arr = [1, 2, [3, 4], 5, [6, 7], 8];
const output = arr.flat(2);
console.log(output); // Output: [1, 2, 3, 4, 5, 6, 7, 8]
```

________________________________________________________________________________________________________________________________________________

```javascript
const a;
console.log(a);
op:
SyntaxError: Missing initializer in const declaration
```
_________________________________________________________________________________________________________________________________________________
```javascript
console.log([] === []);
```
op:
False
_________________________________________________________________________________________________________
```javascript


const obj = {
 a: 1,
b: 2
}
obj.a = 3
console.log(obj)
```

op:
{ a: 3, b: 2 }

______________________________________________________________________________________________________________________________
```javascript

const obj = {
 a: 1,
b: 2
}
const obj2 = {} 
obj = obj2
console.log(obj)
op:
obj = obj2
```

op:
TypeError: Assignment to constant variable.
resolve

______________________________________________________________________________________________________________________________________________________________________________
```javascript

const obj = {
  a: 1,
  b: 2
};
const obj2 = {};
Object.assign(obj, obj2);
console.log(obj);
```

______________________________________________________________________________________________________________________________________________________________________________
```javascript

console.log('ok')
setTimeout(() => {
  console.log("Delayed for 1 second.");
}, 1);
 
setTimeout(() => {
  console.log("Delayed for 0 second.");
}, 0);
```

op:
ok
Delayed for 1 second.
Delayed for 0 second.
-----------------------------------------------------------------------------------------------------------------------
```javascript

console.log('ok')
setTimeout(() => {
  console.log("Delayed for 1 second.");
}, 100);
 
setTimeout(() => {
  console.log("Delayed for 0 second.");
}, 0);
```
op:

ok
Delayed for 0 second.
Delayed for 1 second.


______________________________________________________________________________________________________________________________________________
```javascript

function resolveAfter2Seconds() {
    setTimeout(() => {
      console.log("ok")
    }, 2000);
}
async function asyncCall() {
  console.log('calling');
  const result = await resolveAfter2Seconds();
  console.log(result);
}
asyncCall();
```

op:
calling
undefined
ok

_______________________________________________________________________________________________________________________________


```javascript


function resolveAfter2Seconds() {
    return setTimeout(() => {
      console.log("ok")
    }, 2000);
}
async function asyncCall() {
  console.log('calling');
  const result = await resolveAfter2Seconds();
  console.log(result);
}
asyncCall();
```

OP:
calling
Timeout {
  _idleTimeout: 2000,
  _idlePrev: [TimersList],
  _idleNext: [TimersList],
  _idleStart: 33,
  _onTimeout: [Function (anonymous)],
  _timerArgs: undefined,
  _repeat: null,
  _destroyed: false,
  [Symbol(refed)]: true,
  [Symbol(kHasPrimitive)]: false,
  [Symbol(asyncId)]: 6,
  [Symbol(triggerId)]: 1
}
Ok


____________________________________________________________________________________________________________________________________________
```javascript


function resolveAfter2Seconds() {
      setTimeout(() => {
      console.log("ok")
    }, 2000);
    return 1
}
async function asyncCall() {
  console.log('calling');
  const result = await resolveAfter2Seconds();
  console.log(result);
}
asyncCall();
```

OP:

calling
1
Ok

________________________________________________________________________________________________________________________________________


SORTING
```javascript

function bubbleSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    for (let j = 0; j < n - i - 1; j++) {
      // Swap if the element found is greater than the next element
      if (arr[j] > arr[j + 1]) {
        // Swap arr[j] and arr[j + 1]
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }

  return arr;
}

// Example usage:
const unsortedArray = [64, 34, 25, 12, 22, 11, 90];
const sortedArray = bubbleSort(unsortedArray);

console.log("Unsorted Array:", unsortedArray);
console.log("Sorted Array:", sortedArray);
```

op:
node /tmp/PWwobtYZif.js
Unsorted Array: [
  11, 12, 22, 25,
  34, 64, 90
]
Sorted Array: [
  11, 12, 22, 25,
  34, 64, 90
]

____________________________________________________________________________________________________________________________________

Inbuild method  for sort

```javascript

// Example usage:
const unsortedArray = [64, 34, 25, 12, 22, 11, 90];
const sortedArray = unsortedArray.slice().sort((a, b) => a - b);

console.log("Unsorted Array:", unsortedArray);
console.log("Sorted Array:", sortedArray);
```

op:
Unsorted Array: [
  64, 34, 25, 12,
  22, 11, 90
]
Sorted Array: [
  11, 12, 22, 25,
  34, 64, 90
]


________________________________________________________________________________________________________________________________________________________________
```javascript

// Example array of numbers
const numbers = [5, 2, 9, 1, 5, 6];

// Sorting in ascending order
const ascendingOrder = numbers.slice().sort((a, b) => a - b);
console.log("Ascending Order:", ascendingOrder);

// Sorting in descending order
const descendingOrder = numbers.slice().sort((a, b) => b - a);
console.log("Descending Order:", descendingOrder);

// Sorting an array of objects based on a property
const persons = [
  { name: "John", age: 30 },
  { name: "Alice", age: 25 },
  { name: "Bob", age: 35 }
];

const sortByAge = persons.slice().sort((a, b) => a.age - b.age);
console.log("Sorted by Age:", sortByAge);
```

op:
node /tmp/PWwobtYZif.js
Ascending Order: [ 1, 2, 5, 5, 6, 9 ]
Descending Order: [ 9, 6, 5, 5, 2, 1 ]
Sorted by Age: [
  { name: 'Alice', age: 25 },
  { name: 'John', age: 30 },
  { name: 'Bob', age: 35 }
]


_________________________________________________________________________________________________________
```javascript


const reverseString = function (str) {
    let newString = '';
    for (let i = str.length - 1; i >= 0; i--) {
        newString += str[i];
    }
    return newString;
};

let string = "Bhavik";
let reversedString = reverseString(string);
console.log(reversedString);
```

op:
kivahB
___________________________________________________________________________________________________________________
inbuild method
```javascript

const reverseString = function (str) {
    // Convert the string to an array, reverse it, and then join it back into a string
    return str.split('').reverse().join('');
};
let string = "Bhavik";
let reversedString = reverseString(string);
console.log(reversedString);

```
___________________________________________________________________________________________________________________________________________

searching
```javascript

        let data =[20,40,60,5,10,70,80,99];
        let item=20;
        let index=undefined;

        for(i=0;i<=data.length-1;i++){
            if(data[i]===item)
            {
                index=i;
            
            }
        }
        console.log(index);

```


_______________________________________________________________________________________________________________

```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  var name = 'Lydia';
  let age = 21;
}
//  
sayHi();
```

op:
undefined
ERROR!
  console.log(age)
ReferenceError: Cannot access 'age' before initialization



---------------------------------------------------------------------------------------------------------------------------------- 
```javascript

const myPromise = Promise.resolve(Promise.resolve('Promise'));
 
function funcOne() {
  setTimeout(() => console.log('Timeout 1!'), 0);
  myPromise.then(res => res).then(res => console.log(`${res} 1!`));
  console.log('Last line 1!');
}
funcOne();
```

op:
Last line 1!
Promise 1!
Timeout 1!





_____________________________________________________________________________________________________________________

//const arr = [1, 2, 2 , 3 , 4 , 5, 5, 6]
//output [1, 2, 3, 4, 5 , 6]

```javascript

const arr = [1, 2, 2, 3, 4, 5, 5, 6];
// Use a Set to eliminate duplicates
const uniqueArr = [...new Set(arr)];
console.log(uniqueArr);

```



_____________________________________________________________________________________________________________

● What some function returns in js
```javascript

const numbers = [1, 2, 3, 4, 5];
// Check if at least one element is greater than 3
const hasElementGreaterThanThree = numbers.some(function (element) {
  return element > 3;
});
console.log(hasElementGreaterThanThree);
```

 // Output: true

____________________________________________________________________________________________________________________

What ‘every’ function returns in js
```javascript
const numbers = [1, 2, 3, 4, 5];
// Check if all numbers are less than 10
const allLessThanTen = numbers.every(function (num) {
  return num < 10;
});

console.log(allLessThanTen); 
```

// Output: true



______________________________________________________________________________________________________

Create a function that takes an array of numbers and return "Boom!" if the digit
7 appears in the array. Otherwise, return "there is no 7 in the
array".
sevenBoom([1, 2, 3, 4, 5, 6, 7]) ➞ "Boom!"
// 7 contains the number seven.
sevenBoom([8, 6, 33, 100]) ➞ "there is no 7 in the array"
// None of the items contain 7 within them.
sevenBoom([2, 55, 60, 97, 86]) ➞ "Boom!"
// 97 contains the number seven.

```javascript

>>function sevenBoom(arr) {
  // Convert array elements to strings and join them to create a single string
  const joinedString = arr.join('');

  // Check if the string contains the digit 7
  if (joinedString.includes('7')) {
    return "Boom!";
  } else {
    return "there is no 7 in the array";
  }
}

// Example usage:
console.log(sevenBoom([1, 2, 3, 4, 5, 6, 7])); // Output: "Boom!"
console.log(sevenBoom([8, 6, 33, 100]));       // Output: "there is no 7 in the array"
console.log(sevenBoom([2, 55, 60, 97, 86]));    // Output: "Boom!"


```

op
Boom!
there is no 7 in the array
Boom!

______________________________________
without inbuild


```javascript
// Example usage:


function sevenBoom(arr){
    for(let i = 0; i < arr.length; i++){
        let num =arr[i]
        
        
        while(num > 0){
        if(num % 10 === 7){
            return "Boom"
        }
        num = Math.floor(num / 10)
    }
    }
    return 'there is no 7 in the array'
}
console.log(sevenBoom([1, 2, 3, 4, 5, 6, 7])); // Output: "Boom!"
console.log(sevenBoom([8, 6, 33, 100,7]));       // Output: "there is no 7 in the array"
console.log(sevenBoom([2, 55, 60, 97, 86]));    // Output: "Boom!"

```

_____________________________________________________________________________________________________________________________________________________________________

const arr1 = [

{ "score": 0, "text": "pizza" },

{ "score": 0, "text": "burger" },

{ "score": 0, "text": "paratha" },

{ "score": 0, "text": "samosa" },

{ "score": 0, "text": "other" }

]

const arr2 = ["pizza", "burger", "paratha", "samosa","paneer"];

Result paneer
Return elements of arr2 which are not present in arr1.text

>>
```javascript

const arr1 = [
  { "score": 0, "text": "pizza" },

  { "score": 0, "text": "burger" },

  { "score": 0, "text": "paratha" },

  { "score": 0, "text": "samosa" },

  { "score": 0, "text": "other" }

];

const arr2 = ["pizza", "burger", "paratha", "samosa", "paneer"];

// Filter elements in arr2 that are not present in arr1.text

const result = arr2.filter(item => !arr1.some(obj => obj.text === item));

console.log(result);
```

// Output: ["paneer"]



without inbuild method
```javascript

const arr1 = [
  { "score": 0, "text": "pizza" },
  { "score": 0, "text": "burger" },
  { "score": 0, "text": "paratha" },
  { "score": 0, "text": "samosa" },
  { "score": 0, "text": "other" }
];

const arr2 = ["pizza", "burger", "paratha", "samosa", "paneer"];

function filterManual(arr1, arr2) {
  const result = [];

  // Loop through each item in arr2
  for (let i = 0; i < arr2.length; i++) {
    let found = false;

    // Check if arr2[i] exists in any obj.text in arr1
    for (let j = 0; j < arr1.length; j++) {
      if (arr2[i] === arr1[j].text) {
        found = true;
        break;
      }
    }

    // If not found in arr1, add to result
    if (!found) {
      result.push(arr2[i]);
    }
  }

  return result;
}

const result = filterManual(arr1, arr2);
console.log(result); // Output: ["paneer"]
```



________________________________________________________________________________________________

```javascript

function f1(i) {
  if (i !== 4 && i !== 5) return; // Check if i is neither 4 nor 5, if true, exit the function
  console.log("hello world");     // Print "hello world" if the condition is not met
}

f1(3);  // Call the function with argument 3
f1(4);  // Call the function with argument 4
f1(5);  // Call the function with argument 5
```

op
hello world
hello world





__________________________________________________________________________


```javascript

function FirstFactorial(num) { 
 if (num === 0 || num === 1) {
    return 1;
  } else {
    return num * FirstFactorial(num - 1);
  }
}
   
// keep this function call here 
console.log(FirstFactorial(4)); // Output: 24
console.log(FirstFactorial(8));
```


op:
24
40320

__________________________________________________________________________________________________________________

```javascript

console.log(typeof undefined); // Output: 'undefined'
console.log(typeof null);      // Output: 'object'
console.log(typeof true);      // Output: 'boolean'
console.log(typeof 42);        // Output: 'number'
console.log(typeof 'hello');   // Output: 'string'
console.log(typeof Symbol());  // Output: 'symbol'
console.log(typeof function(){}); // Output: 'function'

// Example of an object
console.log(typeof {});        // Output: 'object'
```

______________________________________________________________________________________
```javascript

function FirstReverse(str) { 
return str.split('').reverse().join('');
}
// Test cases
console.log(FirstReverse("coderbyte"));
```

// Output: etybredoc

_______________________________________________________________________________________________________________________________


Write a JavaScript function to calculate the sum of two numbers.  
```javascript

function addTwoNumbers(num1, num2) {
  return num1 + num2;
}
// Test cases
console.log(addTwoNumbers(5, 3)); // Output: 8
console.log(addTwoNumbers(-2, 7)); // Output: 5
console.log(addTwoNumbers(0, 0)); // Output: 0
```

________________________________________________________________________________________________________________________________
Write a JavaScript function that takes an array of numbers and returns a new array with only the even numbers. 
```javascript

function getEvenNumbers(numbers) {
  return numbers.filter(number => number % 2 === 0);
}
// Example usage:
const numbers = [1, 4, 7, 8, 10, 13];
const evenNumbers = getEvenNumbers(numbers);
console.log("Original array:", numbers);
console.log("Even numbers:", evenNumbers);
```

_____________________________________________________________________________________________________


Write a JavaScript function to check if a given number is prime. 
```javascript


function isPrime(num) {
  if (num <= 1) return false;
  for (let i = 2; i <= Math.sqrt(num); i++)
    if (num % i === 0) return false;
  return true;
}

// Test cases
console.log(isPrime(7));  // Output: true
console.log(isPrime(12)); // Output: false
console.log(isPrime(1));  // Output: false
```



_______________________________________________________________________________________________________________________________________________________________

Implement a function that flattens a nested array in JavaScript, converting it into a single-level array.
```javascript

function flattenArray(arr) {
  let result = [];

  arr.forEach(element => {
    if (Array.isArray(element)) {
      // Recursively flatten nested arrays
      result = result.concat(flattenArray(element));
    } else {
      result.push(element);
    }
  });

  return result;
}

// Test case
const nestedArray = [1, [2, [3, 4], 5], 6, [7, 8]];
const flattenedArray = flattenArray(nestedArray);
console.log(flattenedArray); // Output: [1, 2, 3, 4, 5, 6, 7, 8]


```

_______________________________________________________________________________________________________________________


Given an array of numbers, write a function to find the largest and smallest numbers in the array. 
```javascript

function findMinMax(numbers) {
  if (numbers.length === 0) return "Array is empty";
  return {
    smallest: Math.min(...numbers),
    largest: Math.max(...numbers)
  };
}


// Test case
const numbersArray = [3, 8, 2, 5, 1, 7, 9, 4];
const result = findMinMax(numbersArray);
console.log(result); // Output: { smallest: 1, largest: 9 }

```

 _______________________________________________________________________________________________________________________________________

 
 Write a function that takes an array of integers as input and returns a new array with only the unique elements. 
```javascript

function getUniqueElements(arr) {
  return [...new Set(arr)];
}

// Test case
const inputArray = [1, 2, 3, 4, 2, 3, 5];
const uniqueArray = getUniqueElements(inputArray);
console.log(uniqueArray); // Output: [1, 2, 3, 4, 5]
```

___________________________________________________________________________________________________________________________________________

Implement a function to find the factorial of a given number.
```javascript

function factorial(num) {
  return num <= 1 ? 1 : num * factorial(num - 1);
}
// Test cases
console.log(factorial(4)); // Output: 24
console.log(factorial(8)); // Output: 40320

```

________________________________________________________________________________________________________________________________________
Implement a function to find the sum of all the numbers in an array. 
```javascript

function arraySum(arr) {
  return arr.reduce((sum, num) => sum + num, 0);
}

// Test case
const numbersArray = [1, 2, 3, 4, 5];
const sum = arraySum(numbersArray);
console.log(sum); // Output: 15
```



______________________________________________________________________________________________________________________________________


Given a string, write a function to count the occurrences of each character in the string. 
```javascript

function countCharacters(str) {
  const charCount = {};

  for (let char of str) {
    charCount[char] = (charCount[char] || 0) + 1;
  }

  return charCount;
}

// Test case
const inputString = "programming";
const occurrences = countCharacters(inputString);
console.log(occurrences);
```

______________________________________________________________________________________________________________

Implement a function to remove duplicates from an array
```javascript

function removeDuplicates(arr) {
  return [...new Set(arr)];
}

// Test case
const arrayWithDuplicates = [1, 2, 2, 3, 4, 4, 5];
const arrayWithoutDuplicates = removeDuplicates(arrayWithDuplicates);
console.log(arrayWithoutDuplicates);

```

 __________________________________________________________________________________________________________________________

 
10. Write a function that sorts an array of numbers in ascending order. 
Inbuild method
```javascript


function sortArrayAscending(arr) {
  return arr.slice().sort((a, b) => a - b);
}

// Test case
const unsortedArray = [5, 2, 8, 1, 7];
const sortedArray = sortArrayAscending(unsortedArray);
console.log(sortedArray);
```
_______________________________________________________________________________________________________________________________________________

without inbuild method
```javascript

function sortArrayAscending(arr) {
  const sortedArray = arr.slice(); // Create a copy of the original array
  const len = sortedArray.length;
  
  for (let i = 0; i < len - 1; i++) {
    for (let j = 0; j < len - 1 - i; j++) {
      if (sortedArray[j] > sortedArray[j + 1]) {
        // Swap elements
        const temp = sortedArray[j];
        sortedArray[j] = sortedArray[j + 1];
        sortedArray[j + 1] = temp;
      }
    }
  }
  
  return sortedArray;
}

// Test case
const unsortedArray = [5, 2, 8, 1, 7];
const sortedArray = sortArrayAscending(unsortedArray);
console.log(sortedArray);
```

_____________________________________________________________________________________________________________________________________________


Implement a function that finds the second smallest element in an array of integers. 
```javascript

function findSecondSmallest(arr) {
    // Check if the array has at least two elements
    if (arr.length < 2) {
        return "Array should have at least two elements";
    }

    // Sort the array in ascending order
    arr.sort((a, b) => a - b);

    // The second element will be at index 1 after sorting
    return arr[1];
}

// Example usage
const array = [5,  8, 1, 3];
const secondSmallest = findSecondSmallest(array);
console.log("Second Smallest Element:", secondSmallest); 
```
_______________________________________________________________________________________________

without inbuild method
```javascript

function findSecondSmallest(arr) {
    // Check if the array has at least two elements
    if (arr.length < 2) {
        return "Array should have at least two elements";
    }

    let smallest = arr[0];
    let secondSmallest = arr[1];

    // Iterate through the array starting from the third element
    for (let i = 2; i < arr.length; i++) {
        if (arr[i] < smallest) {
            secondSmallest = smallest;
            smallest = arr[i];
        } else if (arr[i] < secondSmallest && arr[i] !== smallest) {
            secondSmallest = arr[i];
        }
    }

    return secondSmallest;
}

// Example usage
const array = [5, 8, 1, 3];
const secondSmallest = findSecondSmallest(array);
console.log("Second Smallest Element:", secondSmallest);
```


______________________________________________________________________________________________________________________________


Implement a function that returns the average value of numbers in an array. 

```javascript

function calculateAverage(arr) {
  if (arr.length === 0) {
    return "Array is empty";
  }

  const sum = arr.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
  return sum / arr.length;
}

// Test case
const numbersArray = [5, 2, 8, 1, 7];
const average = calculateAverage(numbersArray);
console.log(average);
```
______________________________________________________________________________________________


Write a function that sorts an array of strings in alphabetical order. 
```javascript

function sortStringsAlphabetically(arr) {
  return arr.slice().sort();
}

// Test case
const stringsArray = ['apple', 'orange', 'banana', 'grape'];
const sortedArray = sortStringsAlphabetically(stringsArray);
console.log(sortedArray);
```

__________________________________________________________________________________________


without inbuild function
```javascript

function sortStringsAlphabetically(arr) {
  const sortedArray = arr.slice(); // Create a copy of the original array
  const len = sortedArray.length;
  
  for (let i = 0; i < len - 1; i++) {
    for (let j = 0; j < len - 1 - i; j++) {
      if (sortedArray[j] > sortedArray[j + 1]) {
        // Swap elements
        const temp = sortedArray[j];
        sortedArray[j] = sortedArray[j + 1];
        sortedArray[j + 1] = temp;
      }
    }
  }
  
  return sortedArray;
}

// Test case
const stringsArray = ['apple', 'orange', 'banana', 'grape'];
const sortedArray = sortStringsAlphabetically(stringsArray);
console.log(sortedArray);


```

_______________________________________________________________________



```javascript


(function() {
  var a = b = 5;
})();
console.log(b);

```

op:5


_____________________________________________________________________________________________________________________

```javascript

let abc = {
name: "bhavik",
"age" : 27
  
}
function func(){
console.log(abc.name)
  
}
func(abc)
console.log(abc)
```

op
bhavik"
> Object { name: "bhavik", age: 27 }
_____________________________________________________________________________________________________________________________

// Write a function that performs binary search on a sorted array.
```javascript

function binarySearch(arr, target) {
    let left = 0;
    let right = arr.length - 1;

    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        const midValue = arr[mid];

        if (midValue === target) {
            return mid;  // Element found, return its index
        } else if (midValue < target) {
            left = mid + 1;  // Search the right half
        } else {
            right = mid - 1;  // Search the left half
        }
    }

    return -1;  // Element not found
}

// Example usage:
const sortedArray = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const targetElement = 7;
const resultIndex = binarySearch(sortedArray, targetElement);


if (resultIndex !== -1) {
    console.log(`Element ${targetElement} found at index ${resultIndex}.`);
} else {
    console.log(`Element ${targetElement} not found in the array.`);
}
```
______________________________________________________________________________________________________________


short code
```javascript

function binarySearch(arr, target) {
    let left = 0, right = arr.length - 1;

    while (left <= right) {
        const mid = Math.floor((left + right) / 2);
        if (arr[mid] === target) return mid; // Element found, return its index
        arr[mid] < target ? left = mid + 1 : right = mid - 1; // Adjust search range
    }

    return -1; // Element not found
}

// Example usage:
const sortedArray = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const targetElement = 7;
const resultIndex = binarySearch(sortedArray, targetElement);

console.log(resultIndex !== -1 ? `Element ${targetElement} found at index ${resultIndex}.` : `Element ${targetElement} not found in the array.`);

```

_________________________________________________________________________________________________________


Fibonacci Series js
```javascript

function generateFibonacci(n) {
    let fibonacciSeries = [0, 1];

    for (let i = 2; i < n; i++) {
        let nextNumber = fibonacciSeries[i - 1] + fibonacciSeries[i - 2];
        fibonacciSeries.push(nextNumber);
    }

    return fibonacciSeries;
}

// Example: Generate the first 10 numbers in the Fibonacci series
const result = generateFibonacci(10);
console.log(result); // Output: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]

```
___________________________________________________________________________


Fibonacci Series js

input - 10
output - [0,1,1,2,3,5,8...]
default values - [0,1]

```javascript
function fibonacci(n, defaultValues = [0, 1]) {
    let sequence = defaultValues.slice(0, n);
    if (n <= defaultValues.length) {
        return sequence;
    }
    
    let a = defaultValues[0];
    let b = defaultValues[1];
    for (let i = 2; i < n; i++) {
        let next = a + b;
        sequence.push(next);
        a = b;
        b = next;
    }
    return sequence;
}

// Example usage
const input = 10;
const result = fibonacci(input);
console.log(result); // Output: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```

____________________________________________________________________________
```javascript

let a=10
let b=new Number(10)

console.log(a==b)
console.log(a===b)
op:
true
false

```


________________________________________________________________________________________________

Map
```javascript

const numbers =[1,2,3,4,5]
const squares= numbers.map(square)

console.log(squares)

function square(element){
    return Math.pow(element ,2)
}
```

op:
[ 1, 4, 9, 16, 25 ]



________________________________________________________________________


Filter
```javascript

const number =[1,2,3,4,5]
const evenNums= number.filter(isEven)
const oddNums= number.filter(isodd)

console.log(evenNums)

console.log(oddNums)
function isEven(element ){
    return element % 2 ===0;
}
function isodd(element){
    return element % 2 !==0;
}
```

_____________________________________________________________________________________________


reduce
```javascript

const price =[1,2,3]
const total= price.reduce(sum)
console.log(total)
function sum(acc,e){
    return acc + e
}
```
_____________________________________________________________________________________________


```javascript

function func2(){
 for(var i = 0; i < 3; i++){
  setTimeout(()=> console.log(i),2000);
}
}
func2();
```


op:
3
3
3

____________________________________________________________________________________________________________________
```javascript


function func1(){
 setTimeout(()=>{
  console.log(x);
  console.log(y);
 },3000);
 var x = 2;
 let y = 12;
}
func1();
console.log(2+'-2'+2);
```

op:
2-22

_____________________________________________________________________________________________________________________________________________________________________


This
```javascript

function Person(name, age) {
  this.name = name;
  this.age = age;
}

const person = new Person('hgj', 25);  // Example age, replace with the actual age value
const myage = new Person('Alice', 32); // Example name, replace with the actual name value

console.log(person.name); // Output: John
console.log(person.age);  // Output: 25 (or whatever age you provide)

console.log(myage.name);  // Output: Alice
console.log(myage.age);   // Output: 32
```


op
node /tmp/wh39Ke1gQl.js
John
25
Alice
32

______________________________________________________________________________________________

Call()
```javascript

function greet(name) {
    console.log(`Hello, ${name}! My name is ${this.name}.`);
}

const person = { name: 'John' };

greet.call(person, 'Alice');
// Output: Hello, Alice! My name is John.
```

_____________________________________________________________________________________________________________________

Apply()
```javascript

function greet(name) {
    console.log(`Hello, ${name}! My name is ${this.name}.`);
}

const person = { name: 'John' };

greet.apply(person, ['Alice']);
// Output: Hello, Alice! My name is John.
```

____________________________________________________________________________________________________________
BIND()
```javascript

function greet(name) {
    console.log(`Hello, ${name}! My name is ${this.name}.`);
}

const person = { name: 'John' };
const greetPerson = greet.bind(person, 'Alice');

greetPerson();
// Output: Hello, Alice! My name is John.

```

__________________________________________________________________________________________________________________

```javascript

const salesData = [
  { salesperson: 'John', amount: 100 },
  { salesperson: 'Alice', amount: 150 },
  { salesperson: 'Bob', amount: 200 },
  { salesperson: 'Alice', amount: 120 },
  { salesperson: 'John', amount: 80 },
];
let sale = {};
for (let i = 0; i < salesData.length; i++) {
  if (sale.hasOwnProperty(salesData[i].salesperson)) {
    sale[salesData[i].salesperson] += salesData[i].amount;
  } else {
    sale[salesData[i].salesperson] = salesData[i].amount;
  }
}
 let arr = Object.entries(sale);
 arr.sort((a,b) => {return b[1] - a[1]})
const sortedSale = Object.fromEntries(arr);
console.log(sortedSale)
```

________________________________________________________

inbuild 
```javascript
const salesData = [
  { salesperson: 'John', amount: 100 },
  { salesperson: 'Alice', amount: 150 },
  { salesperson: 'Bob', amount: 200 },
  { salesperson: 'Alice', amount: 120 },
  { salesperson: 'John', amount: 80 },
];

const sortedSale = salesData.reduce((acc, { salesperson, amount }) => {
  acc[salesperson] = (acc[salesperson] || 0) + amount;
  return acc;
}, {});

console.log(sortedSale);
```
__________________________________________________________
```javascript

let arr = [100, 400, 300, 500, 50];
arr.sort((a, b) => {
    return b - a;
});
// Extracting the two maximum numbers
let max1 = arr[0];
let max2 = arr[1];
let result = max1 + max2;
console.log("Max Numbers:", max1, "and", max2);
console.log("Sum of Max Numbers:", result);
```

OP:

Max Numbers: 500 and 400
Sum of Max Numbers: 900

______________________________________________________________________________________________________________________________


```javascript

// Example variable
let myVariable = null;

// Check if the variable is null or undefined
if (myVariable === null || myVariable === undefined) {
  // If it is, assign a default value
  myVariable = " Value";
}

// Use the variable
console.log(myVariable);
```
______________________________________________________________________________________________________________________________________________


Class
```javascript

class Animal {
  // Constructor method is called when an object is instantiated
  constructor(name, species) {
    this.name = name;
    this.species = species;
  }

  // Method to get information about the animal
  getInfo() {
    return `${this.name} is a ${this.species}`;
  }
}

// Creating an instance of the Animal class
const lion = new Animal("Leo", "Lion");

// Accessing the properties and methods of the object
console.log(lion.name);     // Output: Leo
console.log(lion.species);  // Output: Lion
console.log(lion.getInfo()); // Output: Leo is a Lion
```



____________________________________________________________________________________________________________________________________

Inheritance
// Parent class
```javascript

class Animal {
  constructor(name, species) {
    this.name = name;
    this.species = species;
  }
  getInfo() {
    return `${this.name} is a ${this.species}`;
  }
}
// Child class extending the Animal class
class Cat extends Animal {
  constructor(name, breed) {
    // Call the constructor of the parent class (Animal)
    super(name, "Cat");
    this.breed = breed;
  }
  // Override the getInfo method from the parent class
  getInfo() {
    return `${this.name} is a ${this.breed} cat`;
  }
  // Additional method specific to Cat class
  meow() {
    return "Meow!";
  }
}
// Creating an instance of the Cat class
const fluffy = new Cat("Fluffy", "Persian");

// Accessing methods from both parent and child classes
console.log(fluffy.getInfo()); // Output: Fluffy is a Persian cat
console.log(fluffy.meow());     // Output: Meow!
```

__________________________________________________________________________________________________________________________________________________________

Encapsulation in js
```javascript

class Car {
  constructor(make, model) {
    // Private properties
    let _make = make;
    let _model = model;

    // Public method to get make
    this.getMake = function () {
      return _make;
    };

    // Public method to get model
    this.getModel = function () {
      return _model;
    };

    // Public method to set make
    this.setMake = function (newMake) {
      _make = newMake;
    };

    // Public method to set model
    this.setModel = function (newModel) {
      _model = newModel;
    };
  }

  // Public method to get information about the car
  getInfo() {
    return `${this.getMake()} ${this.getModel()}`;
  }
}

// Creating an instance of the Car class
const myCar = new Car("Toyota", "Camry");

// Accessing public methods
console.log(myCar.getInfo());      // Output: Toyota Camry
console.log(myCar.getMake());      // Output: Toyota
console.log(myCar.getModel());     // Output: Camry

// Modifying data through public methods
myCar.setMake("Honda");
myCar.setModel("Accord");

console.log(myCar.getInfo());      // Output: Honda Accord
```


____________________________________________________________________________________________________________________________

Polymorphism in JavaScript
```javascript

class Shape {
  constructor() {
    this.type = "Shape";
  }
  // A method that can be overridden by child classes
  draw() {
    return `Drawing a generic ${this.type}`;
  }
}
class Circle extends Shape {
  constructor(radius) {
    super();
    this.type = "Circle";
    this.radius = radius;
  }
  // Override the draw method of the parent class
  draw() {
    return `Drawing a circle with radius ${this.radius}`;
  }}
class Square extends Shape {
  constructor(sideLength) {
    super();
    this.type = "Square";
    this.sideLength = sideLength;
  }
  // Override the draw method of the parent class
  draw() {
    return `Drawing a square with side length ${this.sideLength}`;
  }}
const shapes = [new Circle(5), new Square(8)];
shapes.forEach(shape => {
  console.log(shape.draw());
})
```

___________________________________________________________________________________________
```javascript

function a () { 
    var b = 10; 
} 
a(); 
console.log(b);
```

op:
node /tmp/6yM2QTsCHI.js
ERROR!
/tmp/6yM2QTsCHI.js:4
 console.log(b);         
             ^
ReferenceError: b is not defined



_____________________________________________________________________________________

```javascript

var a = 10; 
const b= 10; 
console.log(a === b);
```

op
true

____________________________________________________________________________________________________
```javascript


function c () 
{ 
    var d = 20; 
    if(true) 
    {
        let e = 30;
        } 
        console.log(d); 
        console.log(e); 
    
} 
c();
```

op
20
ERROR!
/tmp/a1aZevJPqd.js:9
        console.log(e); 
                    ^

ReferenceError: e is not defined
______________________________________________________________________________________



input: "this is a TseT" 
output: "shit si a TesT"
```javascript

function reverseWords(input) {
    // Split the input string into an array of words
    var words = input.split(' ');

    // Reverse the order of characters in each word
    var reversedWords = words.map(function(word) {
        return word.split('').reverse().join('');
    });

    // Join the reversed words back into a single string
    var output = reversedWords.join(' ');

    return output;
}

// Example usage
var input = "this is a TseT";
var output = reverseWords(input);
console.log(output);
```


___________________________________________________________________________________________________________________________________

// teststring
// t-3
// g-1
```javascript

function getFrequency(string) {
var freq = {};
for (var i=0; i<string.length;i++) {
    var character = string.charAt(i);
    if (freq[character]) {
       freq[character]++;
    } else {
       freq[character] = 1;
    }
}

return freq;
};

let a = getFrequency('teststring');
console.log("a :",a)
```

OP

a : { t: 3, e: 1, s: 2, r: 1, i: 1, n: 1, g: 1 }

__________________________________________________________________________
```javascript


// Code 1:
function runFunc() {
  console.log("1" + 1);            // "11"
  console.log("A" - 1);            // NaN
  console.log(2 + "-2" + 2");      // "2-22"
  console.log("Hello" - "World" + 78); // NaN
  console.log("Hello" + '78");     // "Hello78"
}

runFunc(); // This will execute the function
```

________________________________________________________________
```javascript

// Code 3:
let a = 0;
let b = 'farge'; // Assuming 'farge' is a string
console.log(a == b);  // false
console.log(a === b); // false


```

______________________________________________________________________________________

1 Write a function in JavaScript that takes an array of numbers as input and returns the sum of all the numbers in the array.
2 Your task is to implement this function. You can assume that the input array will always contain numbers.

and find max 

```javascript

function calculateSum(numbers) {
  if (!Array.isArray(numbers)) {
    return "Input is not an array of numbers";
  }
  // Using the reduce method to calculate the sum
  const sum = numbers.reduce((accumulator, currentNumber) => accumulator + currentNumber, 0);
  return sum;
}
// Example usage:
const numbersArray = [1, 2, 3, 4, 5];
const result = calculateSum(numbersArray);
console.log(result); // Output: 15
```


_________________________________________________________________________________________________________________________________________


add(2)(4)(5);
output
total 11 


```javascript

function add(x) {
  // Inner function takes the next number (y) and returns a new function
  const innerFunction = function(y) {
    // Add the current and next numbers
    return add(x + y);
  };

  // Convert the inner function to a primitive when used in a context that expects a primitive
  innerFunction.valueOf = function() {
    return x;
  };

  return innerFunction;
}

// Example usage
const result = add(2)(4)(5);

console.log(result.valueOf()); // Output: 11

```








_____________________________________________________________________________________________________________________________________


const myArray = [2, 7, 1, 8, 4, 5];
const targetSum = 9;
```javascript
function hasPairWithSum(arr, target) {
  const numSet = new Set();
  for (let num of arr) {
    const complement = target - num;
    if (numSet.has(complement)) {
      return true; // Pair found
    }
    numSet.add(num);
  }
  return false; // No pair found
}
const myArray = [2, 7, 1, 8, 4, 5];
const targetSum = 9;
if (hasPairWithSum(myArray, targetSum)) {
  console.log("There is a pair with the sum of 9.");
} else {
  console.log("No pair with the sum of 9 found.");
}

```

Output
OP:
There is a pair with the sum of 9.

___________________________________________________________________________________________________________
Inbuild function
```javascript

function isSumEqualToTarget(arr, target) {
    // Use the reduce method to calculate the sum of the array elements
    const sum = arr.reduce((accumulator, currentValue) => accumulator + currentValue);

    // Check if the sum is equal to the target value
    return sum === target;
}

// Example usage
const numbersArray = [2, 3, 4];
const targetValue = 9;

if (isSumEqualToTarget(numbersArray, targetValue)) {
    console.log('The sum of the numbers in the array is equal to the target value.');
} else {
    console.log('The sum of the numbers in the array is NOT equal to the target value.');
}

```

________________________________________________________________________________________________________________________________
Sort this object
```javascript

const dataObjects = [
  { id: 1, name: 'John', age: 25 },
  { id: 2, name: 'Jane', age: 30 },
  { id: 3, name: 'Bob', age: 22 },
  { id: 4, name: 'Alice', age: 28 },
  { id: 5, name: 'Eva', age: 35 },
  { id: 6, name: 'Charlie', age: 32 },
  { id: 7, name: 'Grace', age: 40 },
  { id: 8, name: 'David', age: 26 },
  { id: 9, name: 'Sophie', age: 27 },
  { id: 10, name: 'Michael', age: 38 },
];

// Custom bubble sort function to sort by age
function bubbleSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    for (let j = 0; j < n - i - 1; j++) {
      if (arr[j].age > arr[j + 1].age) {
        // Swap elements if they are in the wrong order
        const temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }

  return arr;
}
// Sort the dataObjects array using the custom bubble sort function
const sortedDataObjects = bubbleSort(dataObjects);
console.log(sortedDataObjects);
```

____________________________________________________________________________________________________________________________________________________________________
```javascript

const dataObjects = [
  { id: 1, name: 'John', age: 25 },
  { id: 2, name: 'Jane', age: 30 },
  { id: 3, name: 'Bob', age: 22 },
  { id: 4, name: 'Alice', age: 28 },
  { id: 5, name: 'Eva', age: 35 },
  { id: 6, name: 'Charlie', age: 32 },
  { id: 7, name: 'Grace', age: 40 },
  { id: 8, name: 'David', age: 26 },
  { id: 9, name: 'Sophie', age: 27 },
  { id: 10, name: 'Michael', age: 38 },
];

// Use the Array.prototype.sort() method with a custom comparison function
const sortedDataObjects = dataObjects.slice().sort((a, b) => a.age - b.age);

console.log(sortedDataObjects);

```



______________________________________________________________________________________________________________________________________________________

Count the occurrence of keys and convert the result into array of objects where each object belongs to one key and it's occurrence (count). - ---  
[
    { language: 'JavaScript' },{ language: 'JavaScript' },{ language: 'TypeScript' },{ language: 'GoLang' },{ language: 'GoLang' },{ language: 'GoLang' }
]

SHOULD BE CONVERTED TO =

[

{ language: 'JavaScript', count: 2 },

{ language: 'GoLang', count: 3 },

{ language: 'TypeScript', count: 1 },

]
```javascript

var arr = [
    { language: 'JavaScript' },
    { language: 'JavaScript' },
    { language: 'TypeScript' },
    { language: 'GoLang' },
    { language: 'GoLang' },
    { language: 'GoLang' }
];

// Create an object to store the count of each language
var languageCount = {};

// Iterate over the original array and count occurrences
arr.forEach(item => {
    if (languageCount[item.language]) {
        languageCount[item.language]++;
    } else {
        languageCount[item.language] = 1;
    }
});

// Convert the object to the desired array format
var resultArr = Object.keys(languageCount).map(language => ({
    language: language,
    count: languageCount[language]
}));
console.log(resultArr);
```


op:

node /tmp/rXE6MjKX2A.js
[
  { language: 'JavaScript', count: 2 },
  { language: 'TypeScript', count: 1 },
  { language: 'GoLang', count: 3 }
]


_______________________________________________________________________________________________________________
```javascript

let arr = [1, 2, 3, 4, 5, 6, 2, 3, 4, 5];
//let arr= ["a","a","b","b","c","c","c"]

// output = {1: 1, 2: 2, 3: 2, ...}
let duplicate = {};
for (let i = 0; i < arr.length; i++) {
    let count = duplicate[arr[i]] || 0;
    duplicate[arr[i]] = count + 1;
}
console.log(duplicate);
```

op

{ '1': 1, '2': 2, '3': 2, '4': 2, '5': 2, '6': 1 }
_________________________________________________________________________________________

inbuild method
```javascript

let arr = [1, 2, 3, 4, 5, 6, 2, 3, 4, 5];

let duplicate = arr.reduce((acc, value) => {
    acc[value] = (acc[value] || 0) + 1;
    return acc;
}, {});

console.log(duplicate);


```

____________________________________________________________________________________________________________________________________________________________________

5. Implement a function that takes two sorted arrays and merges them into a single sorted array without using any built-in sorting functions. 
```javascript

function mergeSortedArrays(arr1, arr2) {
  const mergedArray = [];
  let i = 0;
  let j = 0;

  // Compare elements from both arrays and merge them in ascending order
  while (i < arr1.length && j < arr2.length) {
    if (arr1[i] < arr2[j]) {
      mergedArray.push(arr1[i]);
      i++;
    } else {
      mergedArray.push(arr2[j]);
      j++;
    }
  }

  // If there are remaining elements in arr1, append them to the merged array
  while (i < arr1.length) {
    mergedArray.push(arr1[i]);
    i++;
  }

  // If there are remaining elements in arr2, append them to the merged array
  while (j < arr2.length) {
    mergedArray.push(arr2[j]);
    j++;
  }

  return mergedArray;
}

// Example usage:
const sortedArray1 = [1, 3, 5, 7];
const sortedArray2 = [2, 4, 6, 8];
const mergedArray = mergeSortedArrays(sortedArray1, sortedArray2);
console.log('Merged and sorted array:', mergedArray);


```

_____________________________________________________________________________________________________________________________________________

Write a function that takes an array of integers as input and returns a new array with only the unique elements. 
```javascript

function getUniqueElements(arr) {
  // Using a Set to store unique elements
  const uniqueSet = new Set(arr);

  // Converting Set back to an array
  const uniqueArray = Array.from(uniqueSet);

  return uniqueArray;
}

// Example usage:
const inputArray = [1, 2, 3, 4, 2, 5, 1, 6];
const uniqueArray = getUniqueElements(inputArray);
console.log('Array with unique elements:', uniqueArray);
```



_____________________________________________________________________________________________________________________________________


How to Check the No of Occurrence of Character in String| in js
```javascript

function countOccurrences(str, char) {
  let count = 0;

  for (let i = 0; i < str.length; i++) {
    if (str[i] === char) {
      count++;
    }
  }

  return count;
}

// Example usage:
const myString = "Hello, World! dad";
const charToCount = "d";
const result = countOccurrences(myString, charToCount);

console.log(`The character '${charToCount}' occurs ${result} times in the string.`);
```

op
The character 'd' occurs 3 times in the string.





_____________________________________________________________________________________________________________________

How to compare two Arrays are Equal or Not in JavaScript
```javascript

function arraysAreEqual(arr1, arr2) {
  return JSON.stringify(arr1) === JSON.stringify(arr2);
}

// Example usage:
const array1 = [1, 2, 3];
const array2 = [1, 2, 3];
const result = arraysAreEqual(array1, array2);

console.log(`Arrays are equal: ${result}`);

```



_______________________________________________________________________________________________________
 
how to swap two variables without using the third|Javascript Coding Interview Question #14
```javascript

let a = 5;
let b = 10;

console.log(`Before swapping: a = ${a}, b = ${b}`);

[a, b] = [b, a];

console.log(`After swapping: a = ${a}, b = ${b}`);

```


_________________________________________________________________________________________________


how to find even or odd numbers in array in javascript 
```javascript

function findEvenOrOddNumbers(arr, type) {
  // type should be 'even' or 'odd'
  const result = arr.filter(number => type === 'even' ? number % 2 === 0 : number % 2 !== 0);
  return result;
}

// Example usage:
const numbersArray = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const evenNumbers = findEvenOrOddNumbers(numbersArray, 'even');
const oddNumbers = findEvenOrOddNumbers(numbersArray, 'odd');

console.log('Even numbers:', evenNumbers);
console.log('Odd numbers:', oddNumbers);
```

______________________________________________________________________________________
```javascript

let a =5
if(a % 2 == 0) {
    console.log("even")
}else {
    console.log("odd")
}
```

___________________________________________________________________________________________________

How to Find missing elements in a given Array 1 to 10
```javascript

const givenArray = [1, 2, 3, 5, 7, 8, 10];
let arr = [];
for(let i=1; i <= 10; i++) {
    if (givenArray.indexOf(i) === -1) {
        arr.push(i);
    }
}
console.log(arr);
```

______________________________________________________________________________________________
```javascript

setTimeout(()=>
console.log(1),0);  

console.log(2);
 
new Promise( res => {  
	console.log(3);  
	res();  
}).then(() => console.log(4));
console.log(5);
```

op
node /tmp/pO4kziiDQU.js
2
3
5
4
1


_______________________________________________________________________________________________________________________________________________


input strs = ["eat","tea","tan","ate","nat","bat"] 
output [["bat"],["nat","tan"],["ate","eat","tea"]]
group anagrams together.
```javascript

function groupAnagrams(strs) {
    const anagramsMap = {};
    
    // Iterate through each string in the array
    for (let str of strs) {
        // Sort the characters of the string to get its signature
        const sortedStr = str.split('').sort().join('');
        
        // If the signature exists in the hashmap, push the original string to its corresponding array
        if (anagramsMap[sortedStr]) {
            anagramsMap[sortedStr].push(str);
        } else {
            // Otherwise, create a new entry in the hashmap
            anagramsMap[sortedStr] = [str];
        }
    }
    
    // Convert the hashmap values into an array and return
    return Object.values(anagramsMap);
}

const strs = ["eat","tea","tan","ate","nat","bat"];
const output = groupAnagrams(strs);
console.log(output);
```

op
[["eat","tea","ate"],["tan","nat"],["bat"]]





__________________________________________________________________________________________________


```javascript

s = "A man, a plan, a canal: 
Panama palindrom or not check js code
const s = 'dad';
const resultval = s.toString().split("").reverse().join('')
console.log(resultval)

if(s===resultval){
    console.log("Palindrome "); 
}else{
    console.log("not Palindrome"); 
}
// Output: true

```




__________________________________________________________________________________________________________

Without inbuild method
```javascript

let a = 'mom';
let newstr = ''
for(let i=a.length -1; i >= 0; i--) {
   newstr +=a[i]; 
}
if(newstr === a) {
    console.log("palindrom");
} else {
    console.log("not palindrom");
}}
```

_________________________________

Q: How do you access the last element of an array?
```javascript

const arr = [1,2,3,4,5,6,7]
const newarr = arr[arr.length-1]
console.log(newarr)
```

___________________________________________________
display name single char if it is more then one bhavikdoshi not display "i" word from bhavik write a code in js 
```javascript

const name = "bhavikdoshi";
const result = name.split("").filter(char => char !== "i").join("");
console.log(result);
```

op
bhavkdosh
_______________________________________________________
```javascript

let str = "bhavikdoshi";
let newstr = "";
for (let i = 0; i < str.length; i++) {
    if (str[i] !== 'i') {
        newstr += str[i];
    }}
console.log(newstr)
```

_____________________________________
```javascript

let employees = [{
    id: 1001,
    department: "IT"
  },
  {
    id: 1002,
    department: "admin"
  },
  {
    id: 1003,
    department: "admin"
  }
];
function getAdminEmployeeIds(employeesArray) {
  return employeesArray.filter(employee => employee.department === "admin").map(employee => employee.id);
}

console.log(getAdminEmployeeIds(employees)); // Output: [1002, 1003]
```

_____________________________________________________________________________________________________________________________________________________________


write a function which will return an array of empty functions and accept an input as length. Use es5.
-> input -> 4 , output -> [f,f,f,f]
```javascript
function createEmptyFunctions(length) {
  var arr = [];
  for (var i = 0; i < length; i++) {
    arr.push('f');
  }
  return arr;
}

// Example usage:
var result = createEmptyFunctions(4);
console.log(result); // Output: ['f', 'f', 'f', 'f']

```



____________________________________________________________________________________________________________________________________________________________________________________

Given a string which includes only letters, write a function that produces the outputs below. 
input = 'abcd'; // 'A-Bb-Ccc-Dddd' 
input = 'cwAt'; // 'C-Ww-Aaa-Tttt'
```javascript
function transformString(input) {
  return input.split('').map((char, index) => char.toUpperCase() + char.toLowerCase().repeat(index)).join('-');
}

// Test cases
console.log(transformString('abcd')); // Output: 'A-Bb-Ccc-Dddd'
console.log(transformString('cwAt')); // Output: 'C-Ww-Aaa-Tttt'
```
__________________________________________________________________________

```javascript
const x = () => {
  console.log("x");
}

function test(y){
  y();
}

test(x);
```

output x
_________________________________________________________________________________________________________________________________________________________________
```javascript

pass by value pass by ref code
function changeValue(x) {
    x = 10;
    console.log("Inside function: ", x); // Output: Inside function: 10
}

var num = 5;
changeValue(num);
console.log("Outside function: ", num); // Output: Outside function: 5
```


___________________________________________________________________________________________________________________________________________________________________
```javascript
function changeProperty(obj) {
    obj.name = "John";
    console.log("Inside function: ", obj); // Output: Inside function: { name: "John" }
}

var person = { name: "Alice" };
changeProperty(person);
console.log("Outside function: ", person); // Output: Outside function: { name: "John" }

```






____________________________________________________________________________________________________________________________________________________________________________________________


arr = [6,,2,4,8,7,3]
target = 10;
show index number
output : [0,2]
```javascript
function findPair(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[i] + arr[j] === target) {
                return [i, j];
            }
        }
    }
    return [];
}

const arr = [6, 2, 4, 8, 7, 3];
const target = 10;

const output = findPair(arr, target);
console.log(output); // Output: [0, 2]
```




_____________________________________________________________________________________________________________________________________________________________________________________________


inpupt [3, 30, 34, 5, 9]


output 9534330

create the largest number by sorting the array in a custom way. Here's how you can implement it in JavaScript:
```javascript
function sort(arr){
  arr= arr.join("").split("");
for(let i=0; i< arr.length; i++) {
    for(let j=i; j< arr.length; j++) {
        if(arr[i] < arr[j]) {
        temp= arr[i];
        arr[i]= arr[j];
        arr[j]=temp;
        }
    }
}
return arr.join('')
}

let arr=[3, 30, 34, 5, 9]
let result = sort(arr)
console.log(result)

```



_________________________________________________________________________________________________________________________________________________________________________________________

Rearrange Array Elements by Sign
Input: nums = [3,1,-2,-5,2,-4]
Output: [3,-2,1,-5,2,-4]
```javascript
let nums = [3, 1, -2, -5, 2, -4];

let positive = [];
let negative = [];
let newArr = [];
for(let i=0; i<nums.length; i++) { 
    if(nums[i] > 0) {
       positive.push(nums[i]) 
    }else {
       negative.push(nums[i]) 
    }
}
for(let p =0; p < Math.max(positive.length,negative.length); p++) {
        newArr.push(positive[p])
        newArr.push(negative[p])
}
console.log(newArr);
```



___________________________________________________________________________________________________________________________________________________________



Median of Two Sorted Arrays

Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```javascript

let nums1 = [1,3], nums2 = [2];
let newArr =nums1.concat(nums2);
newArr.sort(function (a,b) {
    return a-b;
});
let index = Math.floor(newArr.length/2);
console.log(newArr[index]);
```


________________________________________________________________________________________________________________________________________


Reverse Integer

Input: x = 123
Output: 321
```javascript
let arr=[1,2,3]
 arr= arr.join("").split("").reverse();
 arr =arr.join("")
 console.log(arr)
```


__________________________________________________________________________________________________________________________________________________

 Longest Substring Without Repeating Characters 
 ```javascript
function getFrequency(string) {
  var freq = {};
  for (var i = 0; i < string.length; i++) {
    var character = string.charAt(i);
    if (freq[character]) {
      freq[character]++;
    } else {
      freq[character] = 1;
    }
  }
  return freq;
}
let a = getFrequency('abcabcbb');
// let a = getFrequency('pwwkew');
console.log(`The answer is ${Object.keys(a).join('')}, with a length of ${Object.keys(a).length}`);
```

Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.


_______________________________________________________________________________________________________________________________________
```javascript

var isPalindrome = function(x) {
    let a = x.toString(); // Convert the number to a string
    let newstr = '';
    for(let i = a.length - 1; i >= 0; i--) {
        newstr += a[i];
    }
    if(newstr === a) {
        console.log("palindrome");
        return true;
    } else {
        console.log("not palindrome");
        return false;
    }
}

// Test case
let x = 121;
console.log(isPalindrome(x)); // Output: true
```




______________________________________________________________________________________________________________________________________________________

"https://www.google.com/search?q=sdsd&rlz=1C1GCCU_en&oq=sdsd&gs_lcrp=EgZjaHJvbWUyEggAEEUYOR";

// {
//     "q": "sdsd",
//     "rlz": "1C1GCCU_en",
//     "oq": "sdsd",
//     "gs_lcrp": "EgZjaHJvbWUyEggAEEUYOR"
// }

```javascript

var x = "https://www.google.com/search?q=sdsd&rlz=1C1GCCU_en&oq=sdsd&gs_lcrp=EgZjaHJvbWUyEggAEEUYOR";

function parseURLParams(url) {
    var queryParams = {};
    var urlParams = new URLSearchParams(url.split('?')[1]);
    
    urlParams.forEach(function(value, key) {
        queryParams[key] = value;
    });
    
    return queryParams;
}

var result = parseURLParams(x);
console.log(result);
```

__________________________________________________________________________________________________________________________________________________

```javascript
let jsonData = {
  object1: {
    key1: 10,
    key2: 20,
    key3: 10
  },
  object2: {
    key1: 30,
    key2: 10,
    key3: 20
  },
  object3: {
    key1: 40,
    key2: 30,
    key3: 30
  }
};

let obj = {};

for (let object in jsonData) {
  let sum = 0;
  for (let key in jsonData[object]) {
    sum += jsonData[object][key];
  }
  obj[object] = sum;
}

console.log(obj);
```
op
{ object1: 40, object2: 60, object3: 100 }

_____________________________________________________________________________________________________________________________________________________
Given an integer array nums, find the contiguous subarray within the array (containing at least one number) that has the largest product, and print the numbers and the product(a * b). 
let nums1 = [2, 3, -2, 4];
```javascript

let nums1 = [2, 3, -2, 4];
let arr = [];
for(let i=0; i < nums1.length; i++) {
    arr.push(nums1[i] *  nums1[i+1]); 
}
 arr.pop()
console.log(Math.max(...arr))
```
op
6
______________________________________________________________________________________________________________


Multiply Strings

Input: num1 = "2", num2 = "3"
Output: "6"

```javascript
let num1 = "2", 
    num2 = "3";
let result = Number(num1) * Number(num2);
result = result.toString()
console.log(result);

```
op
6
_______________________________________________________________________________________________________________________

Merge k Sorted Lists

Input: lists = [[1,4,5],[1,3,4],[2,6]]

Output: [1,1,2,3,4,4,5,6]

Explanation: The linked-lists are:

[
  1->4->5,
  1->3->4,
  2->6
]

merging them into one sorted list:
1->1->2->3->4->4->5->6

```javascript

let lists = [[1,4,5],[1,3,4],[2,6]];
let arr = Array.prototype.concat.apply([], lists);
arr.sort(function (a,b) {
    return a-b;
})
console.log(arr)

```
op

node /tmp/vTvtkdPEeu.js
[
  1, 1, 2, 3,
  4, 4, 5, 6
]
_______________________________________________________________________

```javascript
function multiply(i, j) {
  console.log("i = " + i);
  console.log("j = " + j);
  console.log("ij = " + (i * j));
}

multiply(30, 40);
```

_____________________________________________________________

Input

Flatten Deeply Nested Array

arr = [1, 2, 3, [4, 5, 6], [7, 8, [9, 10, 11], 12], [13, 14, 15]]

n = 1

Output

[1, 2, 3, 4, 5, 6, 7, 8, [9, 10, 11], 12, 13, 14, 15]

```javascript
var flat = function (arr, n) {
return arr.flat(n);
};

let arr = [1, 2, 3, [4, 5, 6], [7, 8, [9, 10, 11], 12], [13, 14, 15]];
let n = 1;
let flattenedArr = flat(arr,n)
console.log(flattenedArr);
```

_________________________________________________________________________
Combination Sum

Input: candidates = [2,3,6,7],

target = 7

Output: [[2,2,3],[7]]

Explanation:

2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.

7 is a candidate, and 7 = 7.

These are the only two combinations.

```javascript
function combinationSum(candidates, target) {
    const result = [];
    
    function backtrack(remaining, path) {
        if (remaining === 0) {
            result.push(path);
            return;
        }
        
        for (let i = 0; i < candidates.length; i++) {
            if (candidates[i] <= remaining) {
                backtrack(remaining - candidates[i], [...path, candidates[i]]);
            }
        }
    }
    
    backtrack(target, []);
    return result;
}

// Example usage:
const candidates = [2, 3, 6, 7];
const target = 7;
console.log(combinationSum(candidates, target));
```
___________________________________________________________________

```javascript

const express = require("express");
let app = express();
app.use(express.json());
app.post("/factorial" ,(req,res) =>{
let value = req.body.num;
let fact =1;
for (let i =1; i <= value; i++) {
    fact *= i;
}
res.send({result : fact});
})
app.listen(8080);
```
____________________________________________________________________________________________________________________

 Longest Common Prefix

 Input: strs = ["flower","flow","flight"]
Output: "fl"
```javascript

var longestCommonPrefix = function(strs) {
    if (strs.length === 0) return ''; // If the array is empty, return an empty string
    
    let prefix = strs[0]; // Initialize prefix with the first string
    
    // Iterate through the remaining strings
    for (let i = 1; i < strs.length; i++) {
        let j = 0;
        // Compare characters of the current string with the prefix
        while (j < prefix.length && j < strs[i].length && prefix[j] === strs[i][j]) {
            j++;
        }
        prefix = prefix.slice(0, j); // Update prefix to include only the common characters
        if (prefix === '') return ''; // If prefix becomes empty, no common prefix exists
    }
    
    return prefix;
};

// Test case
const strs = ["flower", "flow", "flight"];
console.log(longestCommonPrefix(strs)); // Output: "fl"
```
Output: "fl"
_____________________________________________________________________________________________________________________________________

 Roman to Integer
Input: s = "III"
Output: 3
Explanation: III = 3.
```javascript

function romanToInt(s) {
    // Create a map of Roman numeral characters to their integer values
    const romanToIntMap = {
        'I': 1,
        'V': 5,
        'X': 10,
        'L': 50,
        'C': 100,
        'D': 500,
        'M': 1000
    };

    // Initialize the result variable
    let result = 0;

    // Loop through the Roman numeral string
    for (let i = 0; i < s.length; i++) {
        // Get the integer value of the current character
        const currentValue = romanToIntMap[s[i]];

        // Get the integer value of the next character, if it exists
        const nextValue = romanToIntMap[s[i + 1]];

        // If the current value is less than the next value, subtract it from the result
        if (currentValue < nextValue) {
            result -= currentValue;
        } else {
            // Otherwise, add it to the result
            result += currentValue;
        }
    }

    // Return the final result
    return result;
}

// Test the function with the given example
console.log(romanToInt("III")); // Output: 3
```

_______________________________________________________________________________________________________

Valid Parentheses

Input: s = "()"

Output: true

```javascript

var isValid = function(s) {
    const stack = [];
    const map = {
        '(': ')',
        '{': '}',
        '[': ']'
    };

    for (let char of s) {
        if (char in map) {
            stack.push(char); // Push opening brackets onto the stack
        } else {
            const last = stack.pop(); // Pop the last opening bracket from the stack
            if (char !== map[last]) {
                return false; // If the closing bracket does not match the last opening bracket, return false
            }
        }
    }

    return stack.length === 0; // If the stack is empty, all brackets are valid
};

// Test the function with the given example
console.log(isValid("()")); // Output: true

```
______________________________________________________________________________________________

 Length of Last Word
 
Input: s = "Hello World"

Output: 5

Explanation: The last word is "World" with length 5. js 

```javascript

var lengthOfLastWord = function(s) {
    const words = s.trim().split(' '); // Trim leading and trailing spaces and split the string into words
    return words[words.length - 1].length; // Return the length of the last word
};

// Test the function with the given example
console.log(lengthOfLastWord("Hello World")); // Output: 5
```
__________________________________________________________________________________________

without inbuild method
```javascript

var lengthOfLastWord = function(s) {
    // Trim leading and trailing spaces manually
    let start = 0;
    let end = s.length - 1;
    
    // Find the index of the first non-space character from the beginning
    while (start <= end && s.charAt(start) === ' ') {
        start++;
    }
    
    // Find the index of the first non-space character from the end
    while (end >= start && s.charAt(end) === ' ') {
        end--;
    }
    
    // Find the length of the last word
    let length = 0;
    for (let i = end; i >= start; i--) {
        if (s.charAt(i) === ' ') {
            break; // If a space is encountered, it means the last word has ended
        }
        length++;
    }
    
    return length;
};

// Test the function with the given example
console.log(lengthOfLastWord("Hello World")); // Output: 5
```

____________________________________________________________________________________________________
yt link - https://www.youtube.com/watch?v=C5u_hvbq1qQ&ab_channel=NikhilLohia

here's a JavaScript code snippet that takes an array nums as input and returns an array where each element represents the number of elements smaller than the current element:

// Input: nums = [8,1,2,2,3]

// Output: [4,0,1,1,3]

// 1<=nums[i]<=100

```javascript

function smallerNumbersThanCurrent(nums) {
    const result = [];
    for (let i = 0; i < nums.length; i++) {
        let count = 0;
        for (let j = 0; j < nums.length; j++) {
            if (nums[j] < nums[i]) {
                count++;
            }
        }
        result.push(count);
    }
    return result;
}

const nums = [8, 1, 2, 2, 3];
console.log(smallerNumbersThanCurrent(nums)); // Output: [4, 0, 1, 1, 3]

```
_______________________________________________________________________________________________________________________________

Count Elements With Strictly Smaller and Greater Elements 

Input: nums = [11,7,2,15]

Output: 2

make a short inbuild code js

```javascript

function countElements(nums) {
    let count = 0;
    for (let i = 0; i < nums.length; i++) {
        let smaller = 0, greater = 0;
        for (let j = 0; j < nums.length; j++) {
            if (nums[j] < nums[i]) {
                smaller++;
            } else if (nums[j] > nums[i]) {
                greater++;
            }
        }
        if (smaller > 0 && greater > 0) {
            count++;
        }
    }
    return count;
}

const nums = [11, 7, 2, 15];
console.log(countElements(nums)); // Output: 2
```

__________________________________________________________________________________________________________

Count Pairs Whose Sum is Less than Target

Input: nums = [-1,1,2,3,1], target = 2

Output: 3

Explanation: There are 3 pairs of indices that satisfy the conditions in the statement:

- (0, 1) since 0 < 1 and nums[0] + nums[1] = 0 < target
- 
- (0, 2) since 0 < 2 and nums[0] + nums[2] = 1 < target
- 
- (0, 4) since 0 < 4 and nums[0] + nums[4] = 0 < target
- 
Note that (0, 3) is not counted since nums[0] + nums[3] is not strictly less than the target.]

```javascript


var countPairs = function(nums, target) {
    let count = 0;
    for (let i = 0; i < nums.length; i++) {
        for (let j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] < target) {
                count++;
            }
        }
    }
    return count;
}


const nums = [-1, 1, 2, 3, 1];
const target = 2;
console.log(countPairs(nums, target)); // Output: 3

```

______________________________________________________________________________________________________

 Replace Elements in an Array
 
Input: nums = [1,2,4,6], operations = [[1,3],[4,7],[6,1]]

Output: [3,2,7,1]

Explanation: We perform the following operations on nums:

- Replace the number 1 with 3. nums becomes [3,2,4,6].
- 
- Replace the number 4 with 7. nums becomes [3,2,7,6].
- 
- Replace the number 6 with 1. nums becomes [3,2,7,1].
We return the final array [3,2,7,1].

```javascript

function replaceElements(nums, operations) {
    for (let i = 0; i < operations.length; i++) {
        const [original, replacement] = operations[i];
        const index = nums.indexOf(original);
        if (index !== -1) {
            nums[index] = replacement;
        }
    }
    return nums;
}

const nums = [1, 2, 4, 6];
const operations = [[1, 3], [4, 7], [6, 1]];
console.log(replaceElements(nums, operations)); // Output: [3, 2, 7, 1]
```
_________________________________________________________________________________

Find the Maximum Divisibility Score

Input: nums = [4,7,9,3,9], divisors = [5,2,3]

Output: 3

```javascript

var maxDivScore = function(nums, divisors) {
    let maxScore = 0;

    for (const divisor of divisors) {
        let score = 0;
        for (const num of nums) {
            if (num % divisor === 0) {
                score++;
            }
        }
        maxScore = Math.max(maxScore, score);
    }

    return maxScore;
};

const nums = [4,7,9,3,9]
const divisors =[5,2,3]
console.log(maxDivScore(nums, divisors)); 

```

// Output: 5
_________________________________________________________________________________________________________________________

const input = [1, 0, 3, 0, -1, 0, 6];

const output = [1, 3, -1, 6, 0, 0, 0];

js code sfht all 0 left

```javascript

const input = [1, 0, 3, 0, -1, 0, 6];

function shiftZerosToLeft(arr) {
    let count = 0;
  
    // Iterate through the array
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] !== 0) {
            // Move non-zero elements to the left
            arr[count] = arr[i];
            count++;
        }
    }
  
    // Fill the remaining positions with zeros
    while (count < arr.length) {
        arr[count] = 0;
        count++;
    }
  
    return arr;
}

const output = shiftZerosToLeft(input);
console.log(output); // Output: [1, 3, -1, 6, 0, 0, 0]
```
___________________________________________________________________________________________________________

const input = [9, 9, 9];

output = [1, 0, 0, 0];

```javascript

function plusOne(digits) {
    for (let i = digits.length - 1; i >= 0; i--) {
        if (digits[i] < 9) {
            digits[i]++;
            return digits;
        } else {
            digits[i] = 0;
        }
    }
    // If we're here, it means all digits were 9
    digits.unshift(1);
    return digits;
}

const input = [9, 9, 9];
const output = plusOne(input);
console.log(output); // Output: [1, 0, 0, 0]
```
without inbuilt

```javascript
function plusOne(digits) {
    let carry = 1;
    for (let i = digits.length - 1; i >= 0; i--) {
        const sum = digits[i] + carry;
        digits[i] = sum % 10;
        carry = Math.floor(sum / 10);
        if (carry === 0) {
            // No need to continue if there's no carry
            return digits;
        }
    }
    // If we're here, it means all digits were 9
    digits.unshift(1);
    return digits;
}

const input = [9, 9, 9];
const output = plusOne(input);
console.log(output); // Output: [1, 0, 0, 0]
```
_______________________________________________________________________________________________________________

const input = "I Love Coding"

const output = "I evoL gnidoC"

```javascript

function reverseWords(str) {
    return str.split(' ').map(word => word.split('').reverse().join('')).join(' ');
}

const input = "I Love Coding";
const output = reverseWords(input);
console.log(output);

```
 // Output: "I evoL gnidoC"

without inbuild method
```javascript

function reverseWords(str) {
    let reversed = '';
    let word = '';
  
    for (let i = 0; i <= str.length; i++) {
        if (i === str.length || str[i] === ' ') {
            for (let j = word.length - 1; j >= 0; j--) {
                reversed += word[j];
            }
            if (i !== str.length) {
                reversed += ' ';
            }
            word = '';
        } else {
            word += str[i];
        }
    }
  
    return reversed;
}

const input = "I Love Coding";
const output = reverseWords(input);
console.log(output); // Output: "I evoL gnidoC"

```
_____________________________________________________________________________

shallowcopy

```javascript

const person = {
  name: "Akshay",
  age: 29,
  amounts: [1000, 1001, 1002],
};
// const x = {...person}
const x = Object.assign({}, person);

x.name ="bhavik"
console.log(x)
```

output
{ 
name: 'bhavik', 
age: 29, a
mounts: [ 1000, 1001, 1002 ] 
}

_____________________________________________________________________

deepcopy

```javascript
const person = {
  name: "Akshay",
  age: 29,
  address:{
      city:"state",
      state:"up"
  },
  amounts: [1000, 1001, 1002],
  getName: function () {
      return "all data"
  }
};

const x = JSON.parse(JSON.stringify(person));

x.address.city ="mumbai"
console.log(x)
```

output
{
  name: 'Akshay',
  age: 29,
  address: { city: 'mumbai', state: 'up' },
  amounts: [ 1000, 1001, 1002 ]
}

______________________________________________________________________________________________________
```javascript

var a = 10;
let b = 10
const c = 10;

{
let b = 20;
const c = 30;
console.log(a,b,c)
}
```


op
10 20 30
________________________________________________________________________________________

Please use (for in) to get the max value from an Array, complete the below function:
 
function arrayMax(arr) {
var max = 
 
return max;
};
 ```javascript

function arrayMax(arr) {
    var max = -Infinity; // Initialize max with negative infinity so that any number in the array will be greater than it

    for (var index in arr) {
        if (arr[index] > max) {
            max = arr[index];
        }
    }

    return max;
}

// Example usage:
var myArray = [5, 10, 3, 8, 15, 2];
var maxValue = arrayMax(myArray);
console.log("The maximum value in the array is:", maxValue);

 ```
___________________________________________________________________________________________________

 var words = ['language', 'number', 'developers', 'features', 'browsers’, 'climbing', 'communicate']
 
Please sort this array by the second character of each element.
For example [‘language’, ‘feature’, ‘developer’, ‘climbing’, 'communicate', 'browsers', 'number'] 

 ```javascript

var words = ['language', 'number', 'developers', 'features', 'browsers', 'climbing', 'communicate'];

words.sort(function(a, b) {
    // Extract the second characters of each word
    var charA = a.charAt(1);
    var charB = b.charAt(1);

    // Compare the second characters
    if (charA < charB) {
        return -1;
    } else if (charA > charB) {
        return 1;
    } else {
        // If the second characters are the same, maintain the original order
        return 0;
    }
});

console.log(words);

 ```
______________________________________________________________________________________________________________________________________________________

without inbuild method

 ```javascript

var words = ['language', 'number', 'developers', 'features', 'browsers', 'climbing', 'communicate'];

// Custom sorting function
function sortBySecondCharacter(arr) {
    for (var i = 0; i < arr.length - 1; i++) {
        for (var j = i + 1; j < arr.length; j++) {
            // Compare the second characters of the current and next elements
            var charA = arr[i].charAt(1);
            var charB = arr[j].charAt(1);

            if (charA > charB) {
                // Swap elements if the second character of the current element is greater
                var temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
    return arr;
}

var sortedWords = sortBySecondCharacter(words);
console.log(sortedWords);
 ```
___________________________________________________________________________________
```javascript

console.log("1");

 v = (getDetail("2")) 

console.log(v)

console.log("3");

function getDetail(id){
  setTimeout(async () => {
    console.log(id)
    return await id;
  }, 2000);
  
}
```
OP
```javascript

1
undefined
3
2
```

______________________________________________________________________________________
```javascript

console.log('start');

const promise1 = Promise.resolve().then(() => {
  console.log('promise1');
  const timer2 = setTimeout(() => {
    console.log('timer2')
  }, 0)
});

const timer1 = setTimeout(() => {
  console.log('timer1')
  const promise2 = Promise.resolve().then(() => {
    console.log('promise2')
  })
}, 0)

console.log('end');
```

op
```javascript

start
end
promise1
timer1
promise2
timer2

```

__________________________________________________________________________________
```javascript

for (var i = 0; i < 4; i++) {
    setTimeout((function (num) {
        return function () {
            console.log(num);
        };
    })(i), i * 1000);
}

```
```javascript

op
0
1
2
3
```
_______________________________________________________________________________________

const c = "hello world"

show  "h" in upper case and "w" in uppercase in js use map  in js

```javascript

const c = "hello world";

const result = c.split('').map(char => {
  if (char === 'h'){
    return char.toUpperCase();
  } else if (char === 'w') {
    return 'W';
  } else {
    return char;
  }
}).join('');

console.log(result);

```

________________________________________________________________________________________________________________

curring in js (1)(2)...(n)

```javascript

function generateSequence(n) {
  let sequence = [];
  for (let i = 1; i <= n; i++) {
    sequence.push(i);
  }
  return sequence;
}

console.log(generateSequence(5)); // Output: [1, 2, 3, 4, 5]
```

_____________________________________________________________

```javascript

function mul(a){

  return  function inner1(b){

     return   function inner2(c){

            return a*b*c;

        }

    }

}

console.log(mul(2)(3)(4))
```

__________________________________________________________________________________________________________________________
```javascript

var Employee = {
  company: 'XYZ'
}
 
var emp1 = Object.create(Employee);
console.log(emp1)
delete emp1.company;
console.log(emp1.company)
```
op
{}
XYZ


___________________________________________________________________________________________________________________________

```javascript

console.log(foo)
foo = 1;
 
console.log(foo)
var foo = 1;
 
var foo;
console.log(foo)
foo = 1;
 
foo = 1;
console.log(foo)
var foo;
 
foo();
function foo() {
  console.log('1')
}
 
foo();
var foo = function () {
  console.log('1')
}
```
op

/tmp/main.js:2
console.log(foo)
            ^
ReferenceError: foo is not defined


undefined


undefined


1

1

1

foo();
^

TypeError: foo is not a function
    at Object.<anonymous> (/tmp/main.js:4:1)
_____________________________________________________________________________________________

SUM OF ALL NATURAL NUMBER FROM 1 TO N

```javascript

function mysums(num){
   let sum = 0;
    for(let i=0;i<=num;i++){
        sum=sum +i
    }
    return sum
}
console.log(mysums(5))
console.log(mysums(10))
```
_______________________________________________________________________________________________________
```javascript

function removeDuplicates(array) {
  const uniqueArray = [];
  for (let i = 0; i < array.length; i++) {
    let isDuplicate = false;
    for (let j = 0; j < uniqueArray.length; j++) {
      if (array[i] === uniqueArray[j]) {
        isDuplicate = true;
        break;
      }
    }
    if (!isDuplicate) {
      uniqueArray.push(array[i]);
    }
  }
  return uniqueArray;
}

const array = [1, 2, 2, 3, 4, 4, 5];
const uniqueArray = removeDuplicates(array);
console.log(uniqueArray); // Output: [1, 2, 3, 4, 5]
```


_______________________________________________________________________________________________

sum of digits of a number

```javascript

function sumdigit(num) {
    let sum = 0
    while(num > 0){
        sum+= num % 10
        num = Math.floor(num /10)
    }
    return sum
}
console.log(sumdigit(1287));
```

_____________________________________________________________________________________________

count the number of digits

```javascript
function countDigits(num) {
    num= Math.abs(num)
    let count = 0;
    do{
        count++
        num= Math.floor(num/10)
    }while(num > 0){
        return count
    }
}
console.log(countDigits(12345)); // Output: The number of digits in 12345 is: 5
```
_____________________________________________________________________________________________________

```javascript

const numbers = [1, 2, 4, 6, 3, 7, 8];

const findMissingNumber = (arr) => {
  const n = Math.max(...arr); // Find the maximum number
  const fullSet = Array.from({ length: n }, (_, i) => i + 1); // Create a complete range
  return fullSet.filter(num => !arr.includes(num)); // Find missing numbers
};

console.log(findMissingNumber(numbers));
```

_________________________________________________
missing number

```javascript
function findMissingNumber(arr) {
    // Calculate the expected sum of numbers from 1 to n
    const n = arr.length + 1;
    const expectedSum = (n * (n + 1)) / 2;
    
    // Calculate the actual sum of numbers in the array
    let actualSum = 0;
    for (let i = 0; i < arr.length; i++) {
        actualSum += arr[i];
    }
    
    // The missing number is the difference between the expected sum and the actual sum
    const missingNumber = expectedSum - actualSum;
    
    return missingNumber;
}

// Example usage:
const array = [1, 2, 4, 5, 6];
console.log("Missing number:", findMissingNumber(array)); // Output: 3


```

0p
2
____________________________________________________________________________________________________

```javascript

function myFunction(num) {
    return num * 2;
}

const nums = [1, 2, 3, 4, 5];
const result = nums.map(myFunction);
console.log(result);

```
op
[ 2, 4, 6, 8, 10 ]


______________________________________________________________________________________________________________

```javascript

let a = 1, b = 0, c =4; 
value1 = b || c || a;
console.log(value1);

let x = 3, y = 4, z =0; 
value2 = x && y && z;
console.log(value2);

```
op

4
0

__________________________________________________________________________________________________


remove duplicate value and arrange in accending order in one array
```javascript


const arr1 = [1, 3, 5, 6];
const arr2 = [2, 4, 6];

// Merge and concatenate the arrays
const mergedArray = arr1.concat(arr2);

// Custom bubble sort
function bubbleSort(arr) {
  const length = arr.length;

  for (let i = 0; i < length - 1; i++) {
    for (let j = 0; j < length - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        // Swap elements if they are in the wrong order
        const temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }

  return arr;
}

// Sort the merged array using bubble sort
const sortedArray = bubbleSort(mergedArray);
console.log(sortedArray)

// Remove duplicates
const uniqueArray = sortedArray.filter((value, index, self) => {
    return self.indexOf(value) === index;
  });
  
  console.log(uniqueArray);
```

op

[ 1, 2, 3, 4, 5, 6 ]

_____________________________________________________________________________

const arr = [1,2,3,4]
const arrys = [1,2,6,8]
output 
// 123468
To achieve this without using built-in functions and to remove duplicates while sorting and merging the arrays,

```javascript
function mergeAndSortArrays(array1, array2) {
    // Merged array to hold the elements of both arrays
    let mergedArray = [];
    
    // Merge arrays and remove duplicates
    for (let i = 0; i < array1.length; i++) {
        if (!mergedArray.includes(array1[i])) {
            mergedArray.push(array1[i]);
        }
    }
    for (let i = 0; i < array2.length; i++) {
        if (!mergedArray.includes(array2[i])) {
            mergedArray.push(array2[i]);
        }
    }

    // Sort merged array
    for (let i = 0; i < mergedArray.length; i++) {
        for (let j = i + 1; j < mergedArray.length; j++) {
            if (mergedArray[i] > mergedArray[j]) {
                let temp = mergedArray[i];
                mergedArray[i] = mergedArray[j];
                mergedArray[j] = temp;
            }
        }
    }

    return mergedArray;
}

const arr = [1, 2, 3, 4];
const arrys = [1, 2, 6, 8];

const sortedArray = mergeAndSortArrays(arr, arrys);

// Print the sorted and merged array
console.log(sortedArray.join('')); // Output: 123468

```

___________________________________________________________________________________________________________________


/ Find the first repeating element in an array of integers(*)
// Input:  [10, 5, 3, 4, 3, 5, 6]
// Output: 5


```javascript
function findFirstRepeatingElement(arr) {
    const elementCount = {};

    // Iterate through the array and count occurrences of each element
    for (let i = 0; i < arr.length; i++) {
        const element = arr[i];
        if (elementCount[element]) {
            // If the element is already encountered, it's the first repeating element
            return element;
        } else {
            // Otherwise, mark the element as encountered
            elementCount[element] = 1;
        }
    }

    // If no repeating element found, return null or appropriate message
    return null; // Or any other appropriate indication
}

// Test the function
const arr = [10, 5, 3, 4, 3, 5, 6];
const firstRepeatingElement = findFirstRepeatingElement(arr);
console.log("First repeating element:", firstRepeatingElement);


```

_____________________________________________________________________________________________________________________________________________

input : an awesomeJob
output : na emosewa boJ
```javascript
function reverseWords(input) {
    // Split the input string into an array of words
    let words = input.split(' ');

    // Iterate through each word in the array
    let reversedWords = words.map(word => {
        // Reverse each word
        return word.split('').reverse().join('');
    });

    // Join the reversed words back into a single string
    let reversedString = reversedWords.join(' ');

    return reversedString;
}

// Example usage:
let input = "an awesomeJob";
let output = reverseWords(input);
console.log(output); // Output: "na emosewa boJ"
```
___________________________________________________________________________________

without inbuild
```javascript

function reverseWords(input) {
    let reversedString = ''; // Initialize an empty string to store the reversed string
    let currentWord = ''; // Initialize an empty string to store the current word being built
    
    // Iterate through each character in the input string
    for (let i = 0; i < input.length; i++) {
        // If the current character is not a space, add it to the current word
        if (input[i] !== ' ') {
            currentWord = input[i] + currentWord; // Add the current character at the beginning of the current word
        } else {
            // If it's a space, add the current word to the reversed string and reset the current word
            reversedString += currentWord + ' ';
            currentWord = ''; // Reset currentWord for the next word
        }
    }
    
    // Add the last word (if any) to the reversed string
    reversedString += currentWord;

    return reversedString;
}

// Example usage:
let input = "an awesomeJob";
let output = reverseWords(input);
console.log(output); // Output: "na emosewa boJ"
```

__________________________________________________________________________________________________________

Write a function that finds the longest word in a sentence.

```javascript

function findLongestWord(sentence) {
    // Split the sentence into an array of words
    let words = sentence.split(' ');

    // Initialize a variable to store the longest word
    let longestWord = '';

    // Iterate through each word in the array
    words.forEach(word => {
        // If the current word is longer than the longest word found so far, update the longest word
        if (word.length > longestWord.length) {
            longestWord = word;
        }
    });

    return longestWord;
}

// Example usage:
let sentence = "The quick brown fox jumped over the lazy dog";
let longest = findLongestWord(sentence);
console.log("Longest word:", longest); // Output: "jumped"
```
_______________________________________________________________________

without inbuild method
```javascript

function findLongestWord(sentence) {
    // Initialize variables
    let currentWord = '';
    let longestWord = '';

    // Iterate through each character in the sentence
    for (let i = 0; i < sentence.length; i++) {
        // If the current character is not a space, add it to the current word
        if (sentence[i] !== ' ') {
            currentWord += sentence[i];
        } 
        // If it's a space or the last character in the sentence, check if the current word is longer than the longest word found so far
        if (sentence[i] === ' ' || i === sentence.length - 1) {
            if (currentWord.length > longestWord.length) {
                longestWord = currentWord;
            }
            // Reset the current word for the next word
            currentWord = '';
        }
    }

    return longestWord;
}

// Example usage:
let sentence = "The quick brown fox jumped over the lazy dog";
let longest = findLongestWord(sentence);
console.log("Longest word:", longest); // Output: "jumped"
```


_________________________________________________________________________________________
Write a JavaScript function that takes an array of numbers and returns a new array with only the even numbers.|
```javascript

function filterEvenNumbers(numbers) {
    // Use the filter method to create a new array containing only even numbers
    let evenNumbers = numbers.filter(number => number % 2 === 0);
    
    return evenNumbers;
}

// Example usage:
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evenNumbers = filterEvenNumbers(numbers);
console.log("Even numbers:", evenNumbers); // Output: [2, 4, 6, 8, 10]

```

______________________________________________________________________________________________

without inbuild
```javascript

function filterEvenNumbers(numbers) {
    let evenNumbers = []; // Initialize an empty array to store even numbers
    
    // Iterate through each number in the array
    for (let i = 0; i < numbers.length; i++) {
        // Check if the number is even
        if (numbers[i] % 2 === 0) {
            evenNumbers.push(numbers[i]); // If even, add it to the evenNumbers array
        }
    }
    
    return evenNumbers; // Return the array containing even numbers
}

// Example usage:
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evenNumbers = filterEvenNumbers(numbers);
console.log("Even numbers:", evenNumbers); // Output: [2, 4, 6, 8, 10]
```
___________________________________________________________________________
```javascript
a = [1,2,3];
 b= a;
 c= [...a]
 b.push(4);
 console.log(a,b,c)
```

op
[ 1, 2, 3, 4 ] [ 1, 2, 3, 4 ] [ 1, 2, 3 ]




_______________________________________________________________________________________________________________________________________________

https://leetcode.com/problems/longest-palindromic-substring/

```javascript

function longestPalindrome(s) {
    if (s.length === 0) 
    
    return "";

    let start = 0;
    let end = 0;

    function expandAroundCenter(left, right) {
        while (left >= 0 && right < s.length && s[left] === s[right]) {
            left--;
            right++;
        }
        return [left + 1, right - 1];
    }

    for (let i = 0; i < s.length; i++) {
        let [l1, r1] = expandAroundCenter(i, i);
        let [l2, r2] = expandAroundCenter(i, i + 1);

        if (r1 - l1 > end - start) {
            start = l1;
            end = r1;
        }
        if (r2 - l2 > end - start) {
            start = l2;
            end = r2;
        }
    }

    return s.substring(start, end + 1);
}

// Example usage:
console.log(longestPalindrome("babad")); // Output: "bab" or "aba"
console.log(longestPalindrome("cbbd"));  // Output: "bb"

```

output

bab
bb

_______________________________________________________________________________________________________


https://leetcode.com/problems/add-two-promises/description/

```javascript

var addTwoPromises = async function(promise1, promise2) {
    const [value1, value2] = await Promise.all([promise1, promise2]);
    return value1 + value2;
};

// Example usage:
const promise1 = new Promise(resolve => setTimeout(() => resolve(2), 20));
const promise2 = new Promise(resolve => setTimeout(() => resolve(6), 60));
addTwoPromises(promise1, promise2).then(console.log); // 7
```


_________________________________________________________________________________________________________


// Input [7,3,2,1,3] output [7,3]
// Targets 10 js code
```javascript

function findSubarray(arr, target) {
    for (let i = 0; i < arr.length; i++) {
        let sum = 0;
        for (let j = i; j < arr.length; j++) {
            sum += arr[j];
            if (sum === target) {
                return arr.slice(i, j + 1);
            }
        }
    }
    return [];
}

const inputArray = [7, 3, 2, 1, 3];
const targetSum = 10;
const result = findSubarray(inputArray, targetSum);

console.log(result); // Output: [7, 3]

```
_______________________________________________________________________________________

```javascript

var Input = [ 3,7, 2, 1, 3];
// output [7,3]
// Targets 10 js code
var output = [];
while (output.length < 2) {
  Input.forEach((element) => {
    if (output.length < 1) {
      output.push(element);
    } else if (output.length < 2) {
      if (output[0] + element == 10) {
        output.push(element);
      }
    }
  });
}
console.log("Output", output.sort((a, b) => a + b));

```


_________________________________________________________________________________________________________________

```javascript

console.log('Start');

Promise.resolve().then(() => {
    console.log('Promise Microtask');
});


async function asyncFunction() {
    console.log('Async Function Start');
    await Promise.resolve();
    console.log('Async Function End');
}

asyncFunction();

console.log('End');
 

```

______________________________________________________________________
```javascript

var a = 1
var a = 2
console.log(a)

```
op : 2

____________________________________________________________________
```javascript

let a = 1
let a = 2
console.log(a)


```
op
SyntaxError: Identifier 'a' has already been declared

___________________________________________________________________________
```javascript


console.log("abb" < "ab" == "ab" < "ab"); 
console.log("abb" > "ab" == "ab" < "ab"); 

```
true
false

____________________________________________________________________________

var arr = [2, 3,4,6, 5, 7, 9, 81, 343, 77, 34234]

find a prime number using js

```javascript

// Function to check if a number is prime
function isPrime(num) {
  if (num <= 1) 
  return false;
  if (num === 2) 
  return true;
  for (let i = 2; i <= Math.sqrt(num); i++) {
    if (num % i === 0) {
      return false;
    }
  }
  return true;
}


var arr = [2, 3, 4, 6, 5, 7, 9, 81, 343, 77, 34234];
var primes = arr.filter(isPrime);
console.log(primes); // Output: [2, 3, 5, 7]
```
____________________________________________________________________________

```javascript

let a =5;
let b = 8;
let y=a || b;
let x=a && b;
console.log(x,y);

```
op
8 5

________________________________________________________________________________________________________
 input [“a”,”b”,”c”,”d”,”d”,’e’,”b”,”b”,”c”,”f”,”g”,”h”,”h”,”h”,”e”,”a”]

output  {'a'=>3, 'b'=>2,'c'=>2, 'd'=>2,'e'=>2,'f'=>1,'g'=>1,'h'=>3}

```javascript


const input = ["a", "b", "c", "d", "d", "e", "b", "b", "c", "f", "g", "h", "h", "h", "e", "a"];

const frequency = input.reduce((acc, curr) => {
  acc[curr] = (acc[curr] || 0) + 1;
  return acc;
}, {});

// Format the output as a string with '=>' instead of ':'
const formattedOutput = Object.entries(frequency)
  .map(([key, value]) => `'${key}'=>${value}`)
  .join(', ');

console.log(`{${formattedOutput}}`);

```

op

{'a'=>2, 'b'=>3, 'c'=>2, 'd'=>2, 'e'=>2, 'f'=>1, 'g'=>1, 'h'=>3}

_______________________________________________________________________________


const data = [

  { id: 1, value: [1, 3, 4, 6] },
  { id: 2, value: [4, 3, 10, 9] },
  { id: 3, value: [8, 7, 6, 5] },
  { id: 4, value: [12, 11, 8, 6] }
  
];

 output : [

  { id: 4, value: [12, 11, 8, 6] },
  { id: 2, value: [4, 3, 10, 9] },
 { id: 3, value: [8, 7, 6, 5] },
 { id: 1, value: [1, 3, 4, 6] }

 ]

```javascript

const data = [
  { id: 1, value: [1, 3, 4, 6] },
  { id: 2, value: [4, 3, 10, 9] },
  { id: 3, value: [8, 7, 6, 5] },
  { id: 4, value: [12, 11, 8, 6] }
];

// Sort the array based on the sum of the `value` array in descending order
const sortedData = data.sort((a, b) => {
  const sumA = a.value.reduce((sum, num) => sum + num, 0);
  const sumB = b.value.reduce((sum, num) => sum + num, 0);
  return sumB - sumA; // Sort in descending order
});

console.log(sortedData);
```

// Output:
// [
//   { id: 4, value: [12, 11, 8, 6] },
//   { id: 2, value: [4, 3, 10, 9] },
//   { id: 3, value: [8, 7, 6, 5] },
//   { id: 1, value: [1, 3, 4, 6] }
// ]

_______________________________________________________________________________________________

Array => ["testA", "testB", "testC", "abc"]

SearchString => tes

Output => ["testA","testB","testC"]


```javascript
const array = ["testA", "testB", "testC", "abc"];

const searchString = "tes";

const result = array.filter(item => item.includes(searchString));

console.log(result); // Output: ["testA", "testB", "testC"]

```

___________________________________________________________________________________

without inbild function

```javascript
function strings(array, searchString) {
    const result = [];

    for (let i = 0; i < array.length; i++) {
        const item = array[i];

        // Check if the item contains the searchString
        if (item.indexOf(searchString) !== -1) {
            result.push(item);
        }
    }

    return result; // Return the result array
}

const array = ["testA", "testB", "testC", "abc"];
const searchString = "tes";
const output = strings(array, searchString);
console.log(output); // Output: ["testA", "testB", "testC"]

```



_______________________________________________________________________________________


// i/p = [1,2,3,4,5] and o/p = [4,5,1,2,3]


```javascript

 
 let array = [1,2,3,4,5] 
 let mynewarr = 2
 let newres = array.slice(-mynewarr)
 let newkey = array.slice(0, -mynewarr)
 arr = newres.concat(newkey)
 console.log(arr)
```


_________________________________________

```javascript

(function() {
  console.log(1);
  setTimeout(function() { console.log(2) }, 1000); 
  setTimeout(function() { console.log(3) }, 0); 
  console.log(4);
})();


```

op 
1
4
3
2
________________________________________________________________________

Write a function that checks if a given string is an anagram of another string (contains the same characters in a different order).

```javascript
function areAnagrams(str1, str2) {
    return str1.replace().toLowerCase().split().sort().join('') ===
           str2.replace().toLowerCase().split().sort().join('');
}

// Example usage:
console.log(areAnagrams("ABCD", "silent")); 
console.log(areAnagrams("ABCD", "world"));    


```

OP

true 
false


___________________________________________________________________________
```javascript


console.log(1 +  "2" + "2");
console.log(1 +  +"2" + "2");
console.log(1 +  -"1" + "2");
console.log(+"1" +  "1" + "2");
console.log( "A" - "B" + "2");
console.log( "A" - "B" + 2)

```
op
122
32
02
112
NaN2
NaN
_________________________________________________________________________


```javascript


const array = [10, 20, 30, 40];
const result = array.map((num) => num / 2).filter((num) => num >= 15);
console.log(result)


```

[15, 20]

_______________________________________________
```javascript


let x = Infinity;
console.log(typeof x);
```

op
number

____________________________________________________________

```javascript

let x = 10.5;
let y = parseInt(x);
console.log(y);

```

op

10

______________________________________________________________________

```javascript

let x = 1;
console.log(x + x++);
console.log(x + ++x)

```

op
2
5

________________________________________________________________________
```javascript

let x = [31, 2, 8];
x.sort();
console.log(x);

```
op

[ 2, 31, 8 ]
_________________________________________________________________

```javascript


const a = { b: { c: 2 } };
const b = { ...a };
a.b.c = 3;
console.log(b.b.c);

```
op

3

__________________________________________________________________

```javascript


var trees = ["pine","apple","oak","maple","cherry"];
delete trees[3];
console.log(trees.length);


```

op

5
___________________________________________________________________________________________


What is the result of "10"+20+30 in JavaScript?


op
102030

_________________________________________________________________________

```javascript


var a = [1, 2, 3];
a[10] = 99;
console.log(a[6]);	
```

op

undefined

________________________________________________________________________________

```javascript

let a = [1,2,[3,4,4,5],4];
var b = a;
b[2][1] = 15;
console.log(a);

```

op

[ 1, 2, [ 3, 15, 4, 5 ], 4 ]

______________________________________________________________________________

```javascript

let a = [1,2,[3,4,4,5],4];
var b = a;
b[2] = 15;
console.log(a);

```
op

[ 1, 2, 15, 4 ]

____________________________________________________________________________________


// Input: {2, 10,10, 100, 2, 10, 11,2,11,2}

// Output: 2 10 11

// Input: {5, 40, 1, 40, 100000, 1, 5, 1}

// Output: 5 40 1

```javascript



function removeDuplicatesAndLimitThree(obj) {
  const seen = new Set();
  const result = [];

  for (const item of obj.data) {
    if (!seen.has(item)) {
      seen.add(item);
      result.push(item);
    }
    if (result.length === 3) break; // Stop after 3 unique items
  }

  return result.join(' ');
}


let input1 = { data: [2, 10, 10, 100, 2, 10, 11, 2, 11, 2] };
let input2 = { data: [5, 40, 1, 40, 100000, 1, 5, 1] };

let output1 = removeDuplicatesAndLimitThree(input1);
let output2 = removeDuplicatesAndLimitThree(input2);

console.log(output1); // "2 10 11"
console.log(output2); // "5 40 1"

```
_________________________________________________________________________________________________


Write a code to bundle array elements into set of n elements
  
  Example 1:

  input Array: [1,2,3,4,5,6,7,8,9]

  n = 2
  
  Output: [[1,2],[3,4],[5,6],[7,8],[9]]
  
  Example 2:

  input Array: [1,2,3,4,5,6,7,8,9,10]

  n = 3
  
  Output: [[1,2,3],[4,5,6],[7,8,9],[10]]

```javascript

function bundleArray(arr, n) {
    const result = [];
     for (let i = 0; i < arr.length; i += n) {
    result.push(arr.slice(i, i + n));  
  }
  
  return result;
}
// Example 1
const inputArray1 = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const n1 = 2;
console.log(bundleArray(inputArray1, n1)); // Output: [[1, 2], [3, 4], [5, 6], [7, 8], [9]]

// Example 2
const inputArray2 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const n2 = 3;
console.log(bundleArray(inputArray2, n2)); // Output: [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10]]

```

___________________________________________________________________________

To find the first non-repeated character in a string (like 'swiss'), you can iterate over the string and track the frequency of each character. Then, you can check for the first character that appears only once.

const myStr = 'swiss';
Output  w
Non repeated char str

```javascript

const findFirstNonRepeatedChar = (str) => {
  const charCount = {};

  // Count frequency of each character
  for (let char of str) {
    charCount[char] = (charCount[char] || 0) + 1;
  }

  // Find the first character that occurs only once
  for (let char of str) {
    if (charCount[char] === 1) {
      return char;
    }
  }

  return null; // Return null if no non-repeated character found
}

const myStr = 'swiss';
const result = findFirstNonRepeatedChar(myStr);
console.log(result);  // Output: 'w'
```

__________________________________________________________
```javascript

const x = {
 a: '1',
 b: '2'
};
const y = {
 a: '1',
 b: '2'
}
const z = x;
 
console.log('1' == 1)
console.log('1' === 1)
console.log(x == y)
console.log(x === y)
console.log(z == x)
console.log(z === x)


```


true
false
false
false
true
true


__________________________________________________________________


uppercase

 {
  category1: ['shirt', 'pant'],
  category2: ['shoe', 'slides']
};


```javascript
const categories = {
  category1: ['shirt', 'pant'],
  category2: ['shoe', 'slides']
};

// Transforming the values to uppercase
const category = Object.fromEntries(
  Object.entries(categories).map(([key, value]) => {
    return [key, value.map(e => e.toUpperCase())];
  })
);

console.log(category);

```

op
{ category1: [ 'SHIRT', 'PANT' ], category2: [ 'SHOE', 'SLIDES' ] }


_________________________________________________________________________________

```javascript

console.log(a); 
var a = 5;
console.log(a);
 
console.log(b); 
let b = 10;
```

OP

undefined
5
ERROR!
/tmp/XizQinximy.js:5
console.log(b); 
            ^
ReferenceError: Cannot access 'b' before initialization

____________________________________________________________________________________________

```javascript

foo(); 
function foo() {
console.log("Hello");
}

```

op

Hello

______________________________________________________________________________________________
```javascript

bar();  
var bar = function() {
console.log("World");
};
```

OP

ERROR!
bar();  
^
TypeError: bar is not a function

______________________________________________________________________________________

```javascript

console.log(x); 
var x = 2;
console.log(x); 
```

op
undefined
2
__________________________________________________________________________

```javascript

console.log(a);
console.log(b); 
var a = 1;
let b = 2;

```

op

undefined
ERROR!
console.log(b); 
            ^
ReferenceError: Cannot access 'b' before initialization
______________________________________________________________
```javascript


function example() {
 console.log(c); 
 var c = 3;
 console.log(d); 
 let d = 4;
}

```
op

undefined
ReferenceError: Cannot access 'd' before initialization

_________________________________________________________

```javascript

function outerFunction() {
 console.log(a); 
 var a = 1;
 function innerFunction() {
   console.log(a);
   var a = 2;
 }
 innerFunction();
}
```

op

undefined
undefined

__________________________________________________________________________

```javascript


if (true) {
 console.log(x);
 let x = 10;
}


```
op

ERROR!
/tmp/ahyHp17wk7.js:2
 console.log(x);
             ^

ReferenceError: Cannot access 'x' before initialization

____________________________________________________

To compare the two arrays of objects (ArrObj1 and ArrObj2) based on the id property and add a new property match with the value true if the id matches, you can achieve this by iterating over the two arrays and checking for matches.

```javascript

 const ArrObj1 = [
    { book: "Wellness", author: "Joanne Rowling", id:1001},
    { book: "Health", author: "Marie Lu", id:1002 },
    { book: "fitness", author: "Suzanne Collins", id:1003 },
]
 
 const Arrobj2 = [
    { price: "$110", author: "Joanne Rowling", id:1004},
    { price: "$110", author: "Marie Lu", id:1002 },
    { price: "$130", author: "Suzanne Collins", id:1005 },
]
ArrObj1.forEach(obj1 =>{
    const matcharrayobj = Arrobj2.find(obj2 => obj2.id === obj1.id)
    if(matcharrayobj){
        obj1.match =true
        matcharrayobj.match = true
    }
})
console.log(ArrObj1)
console.log(Arrobj2)

```
op

node /tmp/ztTt2zgx3E.js
[
  { book: 'Wellness', author: 'Joanne Rowling', id: 1001 },
  { book: 'Health', author: 'Marie Lu', id: 1002, match: true },
  { book: 'fitness', author: 'Suzanne Collins', id: 1003 }
]
[
  { price: '$110', author: 'Joanne Rowling', id: 1004 },
  { price: '$110', author: 'Marie Lu', id: 1002, match: true },
  { price: '$130', author: 'Suzanne Collins', id: 1005 }
]

______________________________________________________________________________________________
```javascript

let arr = [2, 4, 3, 1];

let output = arr.map((_, i) => {
  return arr.reduce((acc, val, j) => {
    return i !== j ? acc * val : acc;
  }, 1);
});

console.log(output); 
```

op
 [12, 6, 8, 24]


____________________________________________________________________________________________
To find all possible combinations of elements from the array [10, 20, 30, 40, 50, 60, -10, 0] that sum to 50, we can use a nested loop to check every pair, trio, etc., of numbers. Here's a JavaScript implementation for this task:


```javascript

const arr = [10, 20, 30, 40, 50, 60, -10, 0];
const targetSum = 50;
let result = [];

// Helper function to find combinations that sum to the target
function findCombinations(currentCombo, currentIndex, currentSum) {
  // Base case: if currentSum equals targetSum, add combination to result
  if (currentSum === targetSum) {
    result.push([...currentCombo]);
    return;
  }

  // Iterate over the array from currentIndex onwards
  for (let i = currentIndex; i < arr.length; i++) {
    currentCombo.push(arr[i]);  // Add current element to the combination
    findCombinations(currentCombo, i + 1, currentSum + arr[i]);  // Recursive call
    currentCombo.pop();  // Backtrack and remove the element
  }
}

// Start finding combinations
findCombinations([], 0, 0);

console.log("Combinations that sum to", targetSum, ":", result);
```

op

Combinations that sum to 50 : [
  [ 10, 20, 30, -10 ],
  [ 10, 40 ],
  [ 10, 50, -10 ],
  [ 20, 30 ],
  [ 20, 40, -10 ],
  [ 50 ],
  [ 60, -10 ]
]


__________________________________________________________________________

Not repat without in-built 

```javascript
const array = [2, 4, 1, 0, 10, 8, 12, 9, 8, 1];

// Step 1: Find the largest number
let largest = array[0];
for (let i = 1; i < array.length; i++) {
  if (array[i] > largest) {
    largest = array[i];
  }
}

// Step 2: Find the second largest number
let secondLargest = -Infinity; // Start with a very small number
for (let i = 0; i < array.length; i++) {
  if (array[i] !== largest && array[i] > secondLargest) {
    secondLargest = array[i];
  }
}

console.log(secondLargest);



```

op 
10


______________________________________________________

```javascript

const array = [10, 20, 30, 40];

const result = array
  .map((num) => num * 2) // Fix: num * 2 to multiply each element by 2
  .filter((num) => num >= 15); // Filter the elements that are greater than or equal to 15

console.log(result); // Output the result

```


op
[20, 40, 60, 80]


_________________________________________________________________________

```javascript

function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  return "Hello, my name is " + this.name; // Fix: use this.name
};

var person1 = new Person("Lokesh Pra"); // Fix: complete the string and parentheses
var person2 = new Person("Lucky");

console.log(person1.greet === person2.greet); // Compare the greet methods
```

Op

true

____________________________________________________________________


First number not repeat js

[2, 4, 1, 0, 10, 8, 12, 9, 8, 1]

```


function firstNonRepeating(arr) {
    // Create an object to store the frequency of each number
    const frequency = {};

    // Count the frequency of each number in the array
    arr.forEach(num => {
        frequency[num] = (frequency[num] || 0) + 1;
    });

    // Find the first number with a frequency of 1
    for (let i = 0; i < arr.length; i++) {
        if (frequency[arr[i]] === 1) {
            return arr[i];
        }
    }

    // If no non-repeating number is found, return null
    return null;
}

const numbers = [2, 4, 1, 0, 10, 8, 12, 9, 8, 1];
console.log(firstNonRepeating(numbers)); 
```

op 2
 

_________________________________________________________

i/p= [10,20,40,10,30,40] 
o/p = [10,40]


```javascript

const input = [10, 20, 40, 10, 30, 40];
const output = input.filter((value, index, arr) => arr.indexOf(value) !== index)
                    .filter((value, index, arr) => arr.indexOf(value) === index);

console.log(output); 

```
op

[10, 40]

_______________________________________________________________________
without inbuild
```javascript


const input = [10, 20, 40, 10, 30, 40];
const output = [];
const duplicates = {};

// Loop through the input array to count occurrences
for (let i = 0; i < input.length; i++) {
    const value = input[i];

    // Check if the value is already in the duplicates object
    if (duplicates[value]) {
        duplicates[value] += 1;
    } else {
        duplicates[value] = 1;
    }
}

// Loop through the duplicates object to find values that appear more than once
for (let key in duplicates) {
    if (duplicates[key] > 1) {
        output.push(parseInt(key));
    }
}

console.log(output); 


```

 Output: [10, 40]
_____________________________________________________________________
```javascript

console.log(myVar); 
let myVar = 20;
```
Op

console.log(myVar);
^

ReferenceError: Cannot access 'myVar' before initialization

_____________________________________________________________
```javascript


console.log(myVar);

var myVar = 20;
```

op
undefined

____________________________________________

i/p   AyUsh 

o/p   aYuSH
```javascript


function dynamicCaseChange(str) {
  let result = '';
  
  for (let i = 0; i < str.length; i++) {
    if (i % 2 === 0) {
      result += str[i].toLowerCase(); // Even index: lower case
    } else {
      result += str[i].toUpperCase(); // Odd index: upper case
    }
  }
  
  return result;
}

const result = dynamicCaseChange('aYuSh');
console.log(result); // Output: "dYnSaYuSh"

```

op

aYuSh


__________________________________________________________________________________________
```javascript

let a={};
let b= {key:"b"};
let c= {key:"c"};
a[b] =123;
a[c] =456;
console.log(a[b]);
```


op

456

___________________________________________________________________________________
```javascript


let x= [1,2,3]
let y= [1,2,3]
let z=y;
console.log(x==y);
console.log(x===y);
console.log(z==y);
console.log(z==x);
```

op

false
false
true
false



___________________________________________________________________

```javascript

a = [1]

b = a

b.push(2)

console.log(a,b)
```

op
[ 1, 2 ] [ 1, 2 ]


_______________________________________________
```javascript

a = [1]

b=a

b.push(2)

a.push(3)

console.log(a,b)

```

op
[ 1, 2, 3 ] [ 1, 2, 3 ]


__________________________________________________________________________________
There are some particles in an array : [+5,+10,-5]

the number is showing the mass/size of the particle 
no zero values , either positive / negative 


the sign is the direction in which the particle is moving
+ moving towards right ( 5 ----> )
- moving towards left  (<----- -5 )


+5 ---> ,+10 ----> ,<------- -5
all the particles are having same speed 

Rules for collision: 

If A and B collides and A is greater in mass A will destroy B completely [5 ---->,<---- -10] -> [-10] , [5,-2] -> [5]
If A and B collides and both have same mass they will destroy each other [5 --->,<---- -5] -> []

+10 ---> <----- -12
-12 

```javascript

TEST CASE : 
[5 --> ,<--- -5] => []
[<--- -5,5 ---> ] => [-5,5]
[5 ---> ,<--- -10] => [-10]
[5 ----> ,<---- -3] => [5]
[1 ---> ,2 ---> ,3 ---> ,<--- -4] => [-4]
[-1,3,2 ---> ,<--- -3,1] => [-1,1]
-1,3,-3,1
-1,1
```

```javascript

TEST CASE :

[5,-5] => []

[-5,5] => [-5,5]

[5,-10] => [-10]

[5,-3] => [5]

[1,2,3,-4] => [-4]

[-1,3,2-------3,1] => [-1,1]

[1,3,-3,1]

[1,1]

```


```javascript

function resolveCollisions(arr){
return arr.reduce((stacks , arrs)=>{
  while(stacks.length > 0 && stacks[stacks.length - 1] > 0 && arrs < 0){
    
     const last = stacks.pop()
     if(Math.abs(last) > Math.abs(arrs)){
       stacks.push(last)
       return stacks
     } else if (Math.abs(last) === Math.abs(arrs)) {
        return stacks; 
      }
  }
  stacks.push(arrs);
  return stacks
},[])
}

console.log(resolveCollisions([5, -5]));             
console.log(resolveCollisions([-5, 5]));             
console.log(resolveCollisions([5, -10]));            
console.log(resolveCollisions([5, -3]));            
console.log(resolveCollisions([1, 2, 3, -4]));
console.log(resolveCollisions([-1, 3, 2, -3, 1]));   
console.log(resolveCollisions([-1, 1]));        


```

op

[]
[ -5, 5 ]
[ -10 ]
[ 5 ]
[ -4 ]
[ -1, 1 ]
[ -1, 1 ]

_______________________________________________________________________________________
```javascript

let a = {
  "name": "bhavik"
  
}
let b = {
  ...a
}
b.name = "yash"
console.log(a.name)
```

op

bhavik

____________________________________________
```javascript
function test(){
  salary = 1200
  console.log(salary)
  
}
test()
```
op
1200


____________________________________________________


 finding the length of the longest substring without repeating characters.


Example 2
Input: s = "bbbbb"
Output: 1
Explanation: The longest substring without repeating characters is "b" (only one unique character in the entire string).

Example 3
Input: s = "pwwkew"
Output: 3
Explanation: The longest substring without repeating characters is "wke", which has a length of 3.


```javascript
function lengthOfLongestSubstring(s) {
    let charSet = new Set();
    let left = 0;
    let maxLength = 0;

    for (let right = 0; right < s.length; right++) {
        while (charSet.has(s[right])) {
            charSet.delete(s[left]);
            left++;
        }
        charSet.add(s[right]);
        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}

// Example usage:
console.log(lengthOfLongestSubstring("bbbbb"));  // Output: 1
console.log(lengthOfLongestSubstring("pwwkew")); // Output: 3


```

op 
1
3

____________________________________________________


Example 1:
Input: nums = [3,2,3]
Output: 3
Example 2:
Input: nums = [2,2,1,1,1,2,2]
Output: 2

```javascript

function majorityElement(nums) {
    let count = 0;
    let candidate = null;

    for (let num of nums) {
        if (count === 0) {
            candidate = num;
        }
        count += (num === candidate) ? 1 : -1;
    }

    return candidate;
}

// Example 1
console.log(majorityElement([3, 2, 3])); // Output: 3

// Example 2
console.log(majorityElement([2, 2, 1, 1, 1, 2, 2])); 

```
op 
Output: 2

________________________________________

```javascript


function demo() {
    console.log(a); // Output 1: undefined, because `a` is hoisted (var is hoisted but not initialized).
    console.log(b); // Output 2: ReferenceError, because `b` is not hoisted (let and const are not hoisted like var).
    console.log(c); // Output 3: ReferenceError, because `c` is not hoisted.

    var a = 5;
    let b = 10;
    const c = 15;

    if (true) {
        var a = 50; // This reassigns `a` in the function scope, since var is function-scoped.
        let b = 100; // This `b` is block-scoped and won't affect the outer `b`.
        const c = 150; // This `c` is also block-scoped.

        console.log(a); // Output 4: 50, as `a` is reassigned in the function scope.
        console.log(b); // Output 5: 100, the block-scoped `b` inside the `if` block.
        console.log(c); // Output 6: 150, the block-scoped `c` inside the `if` block.
    }

    console.log(a); // Output 7: 50, as `a` was reassigned to 50 in the function scope.
    console.log(b); // Output 8: 10, as the outer `b` was never modified.
    console.log(c); // Output 9: 15, as the outer `c` was never modified.
}

demo();
```


______________________________________


1. sort the array from mid element in opposite direction
 Given -> [5,6,2, 7, 8, 7, 31]
 Output => [2, 5,6, 7, 31, 8, 7]
```javascript
function sortFromMiddle(arr) {
    const mid = Math.floor(arr.length / 2);
    const middle = arr[mid];
    
    // Separate left and right parts
    let left = [];
    let right = [];
    
    for (let i = 0; i < mid; i++) {
        left.push(arr[i]);
    }
    for (let i = mid + 1; i < arr.length; i++) {
        right.push(arr[i]);
    }

    // Sort left in ascending order
    for (let i = 0; i < left.length - 1; i++) {
        for (let j = i + 1; j < left.length; j++) {
            if (left[i] > left[j]) {
                let temp = left[i];
                left[i] = left[j];
                left[j] = temp;
            }
        }
    }

    // Sort right in descending order
    for (let i = 0; i < right.length - 1; i++) {
        for (let j = i + 1; j < right.length; j++) {
            if (right[i] < right[j]) {
                let temp = right[i];
                right[i] = right[j];
                right[j] = temp;
            }
        }
    }

    // Combine left, middle, and right
    let result = [];
    for (let i = 0; i < left.length; i++) {
        result.push(left[i]);
    }
    result.push(middle);
    for (let i = 0; i < right.length; i++) {
        result.push(right[i]);
    }

    return result;
}

// Test case
const arr = [5, 6, 2, 7, 8, 7, 31];
console.log(sortFromMiddle(arr)); // Output: [2, 5, 6, 7, 31, 8, 7]

```
___________________________________________


Input = [ 
        [0,1,2,2,3,4,5,6,1,1,1], 
        [0,1,2,2,3,4,5,6,1,1,13,14],
        [0,1,2,2,3,4,5,6,1,1,12], 

] 

Write a function where the input are provided. It will return the nested array's index number which have highest number of 1 repeted. js code
```javascript

function findIndexWithMostOnes(arr) {
  let maxCount = 0;
  let indexWithMostOnes = -1;

  arr.forEach((subArray, index) => {
    const count = subArray.reduce((acc, val) => val === 1 ? acc + 1 : acc, 0);
    if (count > maxCount) {
      maxCount = count;
      indexWithMostOnes = index;
    }
  });

  return indexWithMostOnes;
}

// Example usage:
const input = [
  [0,1,2,2,3,4,5,6,1,1,1],
  [0,1,2,2,3,4,5,6,1,1,13,14],
  [0,1,2,2,3,4,5,6,1,1,12],
];

console.log(findIndexWithMostOnes(input)); // Output: 0
```
_________________________________________________________________________________


write a function where some products are in warehouse. Some new request types are coming. If type is "add", products units will be increase with the existing units and if the products type is 'sell', products units will be decrease. After the operation need final products which are in warehouse now.

const products = [
    { name: 'product1', units: 100 },
    { name: 'product2', units: 100 },
    { name: 'product3', units: 100 }
];

const requestTypes = [
    { name: 'product1', units: 100, type: 'add' },
    { name: 'product1', units: 50, type: 'sell' },
    { name: 'product2', units: 30, type: 'add' },
    { name: 'product3', units: 120, type: 'sell' }
];

```javascript

function updateWarehouse(products, requests) {
    const productMap = new Map(products.map(p => [p.name, p.units]));

    requests.forEach(({ name, units, type }) => {
        if (productMap.has(name)) {
            const currentUnits = productMap.get(name);
            productMap.set(name, type === 'add' ? currentUnits + units : Math.max(currentUnits - units, 0));
        }
    });

    return Array.from(productMap, ([name, units]) => ({ name, units }));
}

// Example input
const products = [
    { name: 'product1', units: 100 },
    { name: 'product2', units: 100 },
    { name: 'product3', units: 100 }
];

const requestTypes = [
    { name: 'product1', units: 100, type: 'add' },
    { name: 'product1', units: 50, type: 'sell' },
    { name: 'product2', units: 30, type: 'add' },
    { name: 'product3', units: 120, type: 'sell' }
];

console.log(updateWarehouse(products, requestTypes));

```

_____________________________________________________________________________________

the data structure and show how to set up an Express API to filter and display entries with a roll_no greater than 14.

```javascript

const express = require('express');
const app = express();

// Sample data
const data = [
    { "name": "Arjun Tripathi", "course": "MCA", "roll_no": "14", "id": 1 },
    { "name": "Rahul Durgapal", "course": "MCA", "roll_no": "36", "id": 2 },
    { "name": "Aman Yadav", "course": "MCA", "roll_no": "08", "id": 3 }
];

// Route to filter students with roll_no greater than 14
app.get('/students/roll_no/greater_than_14', (req, res) => {
  const filteredData = data.filter(student => parseInt(student.roll_no, 10) > 14);
  res.json(filteredData);
});


// Start the server
const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});


const express = require('express');
const app = express();

// Sample data
const data = [
    { "name": "Arjun Tripathi", "course": "MCA", "roll_no": "14", "id": 1 },
    { "name": "Rahul Durgapal", "course": "MCA", "roll_no": "36", "id": 2 },
    { "name": "Aman Yadav", "course": "MCA", "roll_no": "08", "id": 3 }
];

// Route to filter students with roll_no greater than 14
app.get('/students/roll_no/greater_than_14', (req, res) => {
  const filteredData = data.filter(student => parseInt(student.roll_no, 10) > 14);
  res.json(filteredData);
});


// Start the server
const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});


```

op

[
  {
    "name": "Rahul Durgapal",
    "course": "MCA",
    "roll_no": "36",
    "id": 2
  }
]

_____________________________________________

"my name is sun"
all this first word capital letter 
output - My Name Is Sun
```javascript
let myname = "my name is sun";

// Capitalize the first letter of each word
let capitalizedName = myname.split(' ').map(word => {
  return word.charAt(0).toUpperCase() + word.slice(1).toLowerCase();
}).join(' ');

console.log(capitalizedName); 


```

output


My Name Is Sun
_________________________________________________
Node js express js api 

Method type: GET Input: [1,2,3,4,5,6,7,8,9]

output: product of numbers in given array
{
  "newarray": 362880
}
 server.js

```javascript

const express = require('express')
const app = express()
const port = 3000


app.get('/newarray', (req,res)=>{
    const numbers = req.query.numbers;

    if (!numbers) {
        return res.status(400).send('Array numbers are required');
    }

const newone = numbers.split(',').map(Number);
const newarray = newone.reduce((one, two) => one * two)
console.log(newarray)

res.json({newarray})

})

app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
})

```

run 
http://localhost:3000/newarray?numbers=1,2,3,4,5,6,7,8,9
_____________________________________
typeof [1,2,3,4]

"object"


___________________________

typeof (function(){})

"function"
__________________________________________________
```javascript

console.log('Start');

setTimeout(() => {  
  console.log('Set Timeout - 1');
  
  Promise.resolve().then(() => {
    console.log('Promise - 1');
  }).then(() => {
    console.log('Promise - 2');
  });

}, 0);

setImmediate(() => {
  console.log('Set Immediate');
});

Promise.resolve().then(() => {
  console.log('Promise - 3');
});

process.nextTick(() => {
  console.log('Next Tick');
  process.nextTick(() => console.log('Next Tick - nested'));
});

console.log('End');
```


op

Start
End
Next Tick
Next Tick - nested
Promise - 3
Set Timeout - 1
Promise - 1
Promise - 2
Set Immediate

____________________________________________________________________________

You are given an array cardPoints where each element represents the points on a card, and an integer k. You are allowed to pick exactly k cards from either end of the array (left or right) to maximize your score. Write a function

input [1, 2, 3, 4, 5, 6, 1];
target k = 3;
output  11

```javascript

function scores(cardPoints, k) {
  const n = cardPoints.length;
  const totalSum = cardPoints.reduce((a, b) => a + b, 0);
  
  if (k === n) return totalSum; // If k equals the length, take all cards
  
  // Find the minimum sum of any subarray of length `n - k`
  const windowSize = n - k;
  let minWindowSum = cardPoints.slice(0, windowSize).reduce((a, b) => a + b, 0);
  let currentWindowSum = minWindowSum;

  for (let i = windowSize; i < n; i++) {
    currentWindowSum += cardPoints[i] - cardPoints[i - windowSize];
    minWindowSum = Math.min(minWindowSum, currentWindowSum);
  }

  // Maximum score by picking `k` cards from both ends
  return totalSum - minWindowSum;
}

const cardPoints = [1, 2, 3, 4, 5, 6, 1];
const k = 3;

console.log(scores(cardPoints, k)); // Expected output: 12

```

____________________________________________________


// Find the Index of the First Occurrence in a String

// Given two strings needle and haystack, return the index of the first occurrence of needle in haystack,
// or -1 if needle is not part of haystack.
// Example 1:

// Input: haystack = "sadbutsad", needle = "sad"
// Output: 0
// Explanation: "sad" occurs at index 0 and 6.
// The first occurrence is at index 0, so we return 0.
// Example 2:

// Input: haystack = "leetcode", needle = "leeto"
// Output: -1
// Explanation: "leeto" did not occur in "leetcode", so we return -1.


```javascript

**
function FirstOccurrence(indexs,twoindexs){
  return indexs.search(twoindexs)
}
console.log(FirstOccurrence("sadbutsad", "sad"))
console.log(FirstOccurrence("leetcode", "leeto"))
```
_______________________________________________________


Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.
Example 1:
Input: x = 123
Output: 321

Example 2:
Input: x = -123
Output: -321

Example 3:
Input: x = 120
Output: 21


```javascript

function reverseInteger(x) {
    const isNegative = x < 0; // Check if the number is negative
    const reversed = parseInt(Math.abs(x).toString().split('').reverse().join('')); // Reverse the digits

    // Handle signed 32-bit integer overflow
    if (reversed > Math.pow(2, 31) - 1) {
        return 0;
    }

    return isNegative ? -reversed : reversed; // Return with the appropriate sign
}

// Example usage:
console.log(reverseInteger(123));  // Output: 321
console.log(reverseInteger(-123)); // Output: -321
console.log(reverseInteger(120));  // Output: 21

```

diff method


```javascript

function reversed(num){
  let rev = 0
  let newrange = num < 0 ? -1 : 1;
  num = Math.abs(num)
  
  while(num !==0){
    rev = rev * 10 + (num % 10);
    num = Math.floor(num/ 10)
  }
  
  rev *= newrange
  
return(rev >= -(2**31) && rev <= (2**31-1)) ? rev:0
}

  console.log(reversed(-123))
    console.log(reversed(123))
        console.log(reversed(120))
```


without inbuild method

```javascript


function reverseInteger(x) {
    let reversed = 0;
    let isNegative = x < 0;

    // Work with the positive value of x
    if (isNegative) {
        x = -x;
    }

    while (x !== 0) {
        // Extract the last digit
        let digit = x % 10;

        // Build the reversed number
        reversed = reversed * 10 + digit;

        // Remove the last digit
        x = (x - digit) / 10;
    }

    // Restore the sign
    if (isNegative) {
        reversed = -reversed;
    }

    // Handle overflow for 32-bit signed integers
    if (reversed > 2147483647 || reversed < -2147483648) {
        return 0;
    }

    return reversed;
}

// Example usage:
console.log(reverseInteger(123));  // Output: 321
console.log(reverseInteger(-123)); // Output: -321
console.log(reverseInteger(120));  // Output: 21

```

__________________________________________________


var events = require('events');
var eventEmitter = new events.EventEmitter();

//Create an event handler:
var myEventHandler = function () {
  console.log('I hear a scream!');
}

//Assign the event handler to an event:
__________________

//Fire the 'event_name' event:
_______________________

write a full code

```javascript
var events = require('events');
var eventEmitter = new events.EventEmitter();

// Create an event handler:
var myEventHandler = function () {
  console.log('I hear a scream!');
};

// Assign the event handler to an event:
eventEmitter.on('scream', myEventHandler);

// Fire the 'scream' event:
eventEmitter.emit('scream');


```
___________________________________
Anagram with two strings

```javascript
function Anagram(str1, str2){
  if(typeof str1 !== 'string' || typeof str2 !== 'string'){

  return false
}
const anagrams = str => str.toLowerCase().replace('').split('').sort().join('')

return anagrams(str1) === anagrams(str2)

}
console.log(Anagram("race", "care"));  // Should return true
console.log(Anagram("race", "hello")); // Should return false```

```

_______________________________________________________

const phone = '7885025909';

/**
 * Output should be exactly the following
 * 0, 2
 * 2, 1
 * 5, 2
 * 7, 1
 * 8, 2
 * 9, 2
 */
function printFormat() {
  //write your code here to get the above output.
}
printFormat();

```javascript

function printFormat() {
  const phone = '7885025909';
  
  // Create an object to store character frequencies
  const frequencyMap = {};
  
  // Count the frequency of each digit
  for (let digit of phone) {
    frequencyMap[digit] = (frequencyMap[digit] || 0) + 1;
  }
  
  // Sort the entries to match the required output order
  const sortedEntries = Object.entries(frequencyMap)
    .sort((a, b) => a[0].localeCompare(b[0]));
  
  // Print in the specified format
  sortedEntries.forEach(([digit, count]) => {
    console.log(`${digit}, ${count}`);
  });
}

printFormat();


```
__________________________________________________
To filter out objects where the name contains the letter 'a' in any part of the string,

const array = [

  { name: 'apple' },

  { name: 'banana' },

  { name: 'kiwi' },

  { name: 'melon' },

  { name: 'avocado' },
];

output
 
{ name: 'kiwi' },

{ name: 'melon' },

```javascript

const array = [
  { name: 'apple' },
  { name: 'banana' },
  { name: 'kiwi' },
  { name: 'melon' },
  { name: 'avocado' },
];

const filteredArray = array.filter((item) => !item.name.includes('a'));

console.log(filteredArray);

```

_______________________________________________________________
kiwi and melon first capital letter
const array = [
  { name: 'apple' },

  { name: 'banana' },

  { name: 'kiwi' },

  { name: 'melon' },

  { name: 'avocado' },
];


output
[ { name: 'Kiwi' }, 

{ name: 'Melon' } ]


```javascript

const array = [
  { name: 'apple' },
  { name: 'banana' },
  { name: 'kiwi' },
  { name: 'melon' },
  { name: 'avocado' },
];

const filteredArray = array
  .filter((item) => !item.name.includes('a'))
  .map(item => {
    if (item.name === 'kiwi') {
      return { ...item, name: 'Kiwi' };
    }
    if (item.name === 'melon') {
      return { ...item, name: 'Melon' };
    }
    return item;
  });

console.log(filteredArray);
```


__________________________________________



calculate the sum of all numeric digits in the string "abc6hki9", you can loop through the string, identify the digits, and add them together. 
```javascript

let str = "abc6hki9";
let sum = 0;

// Loop through the string to find digits
for (let i = 0; i < str.length; i++) {
  let char = str[i];

  // Check if the character is a digit
  if (!isNaN(char) && char !== ' ') {
    sum += parseInt(char);
  }
}

console.log(sum);  // Output: 15

```


____________________________________________________

/Write a program which returns all start position of input substring occurs in a string.

// e.g. str = 'As sly as a fox, as strong as an ox,


```javascript

function findSubstringPositions(str, subStr) {
  let positions = [];
  let index = str.indexOf(subStr);  // Start from the first occurrence of the substring

  while (index !== -1) {
    positions.push(index);         // Store the position
    index = str.indexOf(subStr, index + 1);  // Search for the next occurrence
  }

  return positions;
}

// Example usage
const str = 'As sly as a fox, as strong as an ox,';
const subStr = 'as';
const positions = findSubstringPositions(str, subStr);

console.log("Positions:", positions);



```

op
Positions: [ 7, 17, 27 ]

_________________________________________________________________

let a = 5;
let b = 10;

value of a & b without using third variable, it Id work for both interger and string values.

```javascript

let a = "test1";
let b = "test2";

// Swap without a third variable using template literals
a = [b, b = a][0];  // swap values using destructuring

console.log("a:", a);  // "test2"
console.log("b:", b);  // "test1"

```

_____________________________________________________________________


const data = [3,5,6,1,9,7,8,4],

// find second smallest

// find second largest

// dont use sort method.

Js code without in-built 


```javascript

const data = [3, 5, 6, 1, 9, 7, 8, 4];

// Find second smallest
let smallest = Infinity;
let secondSmallest = Infinity;

for (let i = 0; i < data.length; i++) {
  if (data[i] < smallest) {
    secondSmallest = smallest;
    smallest = data[i];
  } else if (data[i] < secondSmallest && data[i] !== smallest) {
    secondSmallest = data[i];
  }
}

// Find second largest
let largest = -Infinity;
let secondLargest = -Infinity;

for (let i = 0; i < data.length; i++) {
  if (data[i] > largest) {
    secondLargest = largest;
    largest = data[i];
  } else if (data[i] > secondLargest && data[i] !== largest) {
    secondLargest = data[i];
  }
}

console.log("Second Smallest:", secondSmallest);
console.log("Second Largest:", secondLargest);




```
op
3
8

____________________________________________________________________



which checks for all brackets are balanced or not. 
   Similarly write a function that will check if the given string is having all the brackets are closed.
Example:
a.
Input: "function sample (args) { const arr=[]; return arr; }"
Output: TRUE
b.
Input: "function sample(args)) { const arr=[]; return arr; }"
Output: FALSE
c.
Input: "function sample(args) { const arr=[]; return arr;"
Output: FALSE
d.
Input: "function sample(args) { const arr=[[[]; return arr; }"
Output: FALSE



```javascript
function areBracketsClosed(args){
    const mysample = []
    const bracks ={
        ')' : '(',
        '}': '{',
        ']': '['
    }
    for(let i = 0; i < args.length;i++){
        const char = args[i]
        
        
        if(char === '(' || char === '{' || char === '['){
            mysample.push(char)
        }
        else if(char === ')' || char === '}' ||  char === ']'){
            if(mysample.length === 0 || mysample.pop() !== bracks[char]){
                return false
            }
        }
    }
    return mysample.length === 0
}

console.log(areBracketsClosed("function sample (args) { const arr=[]; return arr; }"));   // Output: "TRUE"
console.log(areBracketsClosed("function sample(args)) { const arr=[]; return arr; }"));  // Output: "FALSE"
console.log(areBracketsClosed("function sample(args) { const arr=[]; return arr;"));    // Output: "FALSE"
console.log(areBracketsClosed("function sample(args) { const arr=[[[]; return arr; }")); // Output: "FALSE"
 



```
____________________________________________________________________

find the missing numbers between the smallest and largest numbers in an array of 10 numbers,
```javascript

let arr = [5, 3, 8, 10, 14, 5, 7, 15, 17, 12];
Missing numbers: [4, 6, 9, 11, 13, 16]


```javascript



function findMissingNumbers(arr) {
  // Find the smallest and largest numbers in the array
  let min = Math.min(...arr);
  let max = Math.max(...arr);
  
  // Create an array for the full range of numbers
  let fullRange = [];
  for (let i = min; i <= max; i++) {
    fullRange.push(i);
  }

  // Filter the full range to find numbers not in the original array
  let missingNumbers = fullRange.filter(num => !arr.includes(num));

  return missingNumbers;
}

// Example input
let arr = [3, 7, 1, 9, 5, 4, 8, 6, 2];
let missing = findMissingNumbers(arr);

console.log("Missing numbers:", missing);

```


____________________________________________
let arr = [1, 2, 3, 1, 2, 2, 4, 3];
OUTPUT { '1': 2, '2': 3, '3': 2, '4': 1 }


```javascript

let arr = [1, 2, 3, 1, 2, 2, 4, 3];

function countOccurrences(array) {
  let counts = {}; // Object to store element frequencies

  for (let i = 0; i < array.length; i++) {
    let currentElement = array[i];
    if (counts[currentElement] === undefined) {
      counts[currentElement] = 1; // First occurrence of the element
    } else {
      counts[currentElement]++; // Increment the count for repeated element
    }
  }

  return counts; // Return the counts object
}

let result = countOccurrences(arr);
console.log(result);
```

OP


{ '1': 2, '2': 3, '3': 2, '4': 1 }
_________________________________________________________________

Function outer(){

function inner() {

return "hello"

5

}

return inner

}

How can we return hello how we call


```javascript

function outer() {
  function inner() {
    return "hello";
  }
  return inner;  // outer returns the inner function
}

const returnedFunction = outer();  // Call outer to get the inner function
console.log(returnedFunction());   // Call the inner function to get "hello"

```

___________________________________________________________
```javascript

x = 10

console.log(x)

var x
```


OP 
10
____________________________________________________

```javascript

function* myGenFunc() {
  yield 1;
  yield 2;
  yield 3;
}

var myGenObj = myGenFunc();  // Call the generator function directly

console.log(myGenObj.next().value);  


```
OP
1
______________________________________________________
```javascript

console.log("🙂" === "🙂");
```

OP 

TRUE

_________________________________________________________________________

```javascript

const squareObj = new Square(10);
console.log(squareObj.area);

class Square {
  constructor(length) {
    this.length = length;
  }

  get area() {
    return this.length * this.length;
  }

  set area(value) {
    this.area = value;
  }
}

```

OP

const squareObj = new Square(10);
                  ^

ReferenceError: Cannot access 'Square' before initialization

FIX

```javascript


class Square {
  constructor(length) {
    this.length = length;
  }

  get area() {
    return this.length * this.length;
  }

  set area(value) {
    this.area = value;
  }
}
const squareObj = new Square(10);
console.log(squareObj.area);

```
op

10

