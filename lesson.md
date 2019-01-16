# Intro to Recursion

In this lesson, we'll be discussing a new programming topic called Recursion. Recursion allows a program to repeat a process until a specific condition is reached, but with more flexibility and power than a while loop. Recursion is a useful alternative to iteration methods like for loops and while loops, especially for problems that analyze all possible combinations, or permutations, of a given input. The methods of advanced data structures will often rely on recursion as well, so recursion is an important tool to have moving forward. Recursion will challenge the way you analyze and track the progress of a function as it runs, so be prepared to exercise your analytical skills in diagramming how recursive functions run.

---

## Definition

Recursion is when a function calls itself.

The most direct definition of a recursive function is one that calls itself. We know that a function can call upon other functions to achieve its goal. When your functions start getting too big to read clearly and test easily, you split them up into smaller functions that each perform part of the larger task. A recursive function, however, will achieve a small part of the larger task, then pass the partially completed problem to another call of itself. Let's take a look at a simple recursive function to explain this process.

---

### A recursive function

```javascript
function countDown(num){
  if(num < 0){
    return;
  }
  console.log(num)
  return countDown(num - 1)
}
```

Here we have a recursive function that counts down from a given number to 0. Notice how the last part of the function calls itself, but with a slightly different argument than the number initially given. This is what makes the function recursive. Let's work through how this function would operate if we called it with 3 as our argument.

---
#### The Base Case 

```javascript
function countDown(num){
  if(num < 0){
    return;
  }
}
```

The base case establishes when the recursive function can finally return a specific value.

First, we check if the number given is less than zero. This is our base case, which checks if the recursive function can stop calling itself. This is usually when the function has a specific value to return, instead of needing another recursive call to figure out the return value. Since 3 is not less than zero, we can proceed, but once we get below zero, the countdown is over and the function can complete by returning. Typically, we would return some kind of computed value, but a countdown has no answer to return, so we simply return.

---
#### The Action

```javascript
function countDown(num){
  if(num < 0){
    return;
  }
  console.log(num)
}
```

Between the base case and recursion, the function performs an action.

Next, we perform the action of our function. In this case, we simply want to count each number before proceeding to the next one, so we console log the number the function is given.

---
#### The Recursive Case

```javascript
function countDown(num){
  if(num < 0){
    return;
  }
  console.log(num)
  return countDown(num - 1)
}
```

The recursive case calls the function again, with an argument that gets closer to the base case.

Finally, we use recursion by calling the countDown function again. Only this time, we feed it the next number in the sequence, by providing num minus one as the argument. So, after initially counting the number 3, the countDown function gets called again with 2 as the given number. The function will check to make sure that 2 is still greater than zero, count the number 2, and call countDown again with 1. That function will check 1 against zero, console log 1, and call countDown with zero. The countDown will confirm that 0 isn't less than 0, count the number 0, and call countDown again with negative one as the given number. Finally, the base case occurs- the if check realizes we've gone past 0 and are into negative numbers, and simply returns to stop the sequence, instead of continuing on with the next few steps.

---

### Three steps of recursion

1. Base case
2. Action
3. Recursive case leading towards the base case

We can break down the process of a recursive function into three steps. First, establish a base case- when do we know the process can stop? At this point we can return a specific value, instead of recursing and calling the function again.

Then, perform the action of the function. If recursive functions simply called themselves forever without doing anything extra, they wouldn't be very useful. In our countdown function, all we did was console log the number, but regular recursive functions will do some kind of computation that helps build up the end result.

Finally, we call the recursive function again, being very careful to make sure we make progress towards the base case. If we hadn't subtracted one from the number in our recursive case, for example, then countDown would console.log the same number over and over again, never reaching the base case, and leading to an infinite process. Eventually, this will cause a stack overflow when the stack of unresolved function calls gets too large to handle.

---

## Writing recursive functions

First, define your function and parameters.

```javascript
function sumArrayOfNums(arr, index, sum){
}
```

For this example, we'll write a function that sums all the numbers inside of an array. Anything you need to keep track of throughout the recursive process should be included as a parameter, so each recursive call can use the progress made so far. In this case, we need to keep track of what index we're at, and the sum of the numbers so far, in addition to the original array passed in.

---

Define your base case and return the computed result.

```javascript
function sumArrayOfNums(arr, index, sum){
  if(index === arr.length){
      return sum;
  }
}
```

In this case, we know the function can return the sum when the index has gone past the end of the array.

---

Perform the action step.

```javascript
function sumArrayOfNums(arr, index, sum){
  if(index === arr.length){
      return sum;
  }
  sum += arr[index];
}
```

Our action step is adding the number at the current index in the array to the sum variable.

---

Finally, return the function again, with new arguments to make progress towards the base case.

```javascript
function sumArrayOfNums(arr, index, sum){
  if(index === arr.length){
      return sum;
  }
  sum += arr[index];
  return sumArrayOfNums(arr, index + 1, sum);
}
```
Make sure that you RETURN the recursive function call, otherwise the final return value won't return beyond the scope of the second-to-last recursive call. Each recursive call needs to return the value of the next call, so the end result gets passed back up the chain to the very first call of the function.

You might be thinking, couldn't we just do this with a for loop? The answer is yes, and a for loop would still be the clearest way to solve this particular problem. The purpose of this example is to expose you to recursive concepts using a familiar pattern and problem, but later challenges will make more sense recursively than iteratively.

---
## Default parameters

To call this function as-is, we would have to pass it three arguments:

```javascript
const total = sumArrayOfNums(myArray, 0, 0);
```

However, index and sum are always going to start at 0. We should be able to use the function like this instead:

```javascript
const total = sumArrayOfNums(myArray);
```

With recursive functions, it can be useful to give your parameters default values:

```javascript
function sumArrayOfNums(arr, index = 0, sum = 0){
}
```

In this example, the index and sum can both always start at zero. When defined this way, they don't need to be provided when calling the function.

---
# Applications of Recursion

- Permutations
- Traversing Multiple Paths
- Divide and Conquer

Now that we know about how recursion works, let's talk about when and why we would use it. First, we should understand that any recursive function can be written using iteration, and iteration will typically be more efficient than recursion. Recursion is useful because it allows for more straightforward, elegant code to solve complex problems. 

You should think about using recursion in any situation that requires exploring multiple possibilities or paths, such as calculating all possible combinations of elements, or checking all paths between two destinations. Recursion provides the simplest solution by allowing a function to continue through each possibility in a new recursive call.

Recursion also lets us divide a larger problem into smaller subproblems. For example, Merge sort can recursively break down the problem of sorting an array into sorting two, smaller arrays, then recombining them. Eventually, it will reach the base case of a single element array, and zip these single-element arrays back together into a complete, sorted array. While this process could be done using iteration, it would become unweildy and difficult to read, modify, or debug compared to the recursive version.

# Conclusion

- A recursive function calls itself until a solution is reached
- Recursive functions have a base case, action, and recursive case
- Recursion is useful for permutation and divide and conquer problems