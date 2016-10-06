# The Alternative
*(or how to write boolet proof code when no bullets are flying around)*

There was an `if` and it evaluating it's condition.

```cs
if (condition){
    // do the work 
}
```

And somebody wanted to do something else, if the condition was not satisfied. So, he needed a way of knowing if the `if` block was executed or not.

And, as it was deep in the night (the time monsters appear), this was born:

```cs
bool isHandeled = false;

if (condition){
    // do the work
    isHandeled = true;
}

if (!isHandeled){
    // do the other work
}
```

Unit tests were written, and the behaviour was as expected. The problem was with the requirements. They did what they knew better, and that is to grow. So a new condition was born. 

```cs
bool isHandeled = false;

if (condition){
    // do the work
    isHandeled = true;
}

if (!isHandeled && newCondition){
    // do the other work
}
```

Everything was fine. That ment, that the allready proven working pattern could be resused by others:

```cs
bool isHandeled = false;

if (condition){
    // do the work
    isHandeled = true;
}

if (!isHandeled && newCondition1){
    // do the other work
    isHandeled = true;
}

if (!isHandeled && newCondition2) {
    // do completeley different work
    isHandeled = true;
}
```

One day, one funny thing happened. The conditions needed to be reordered. So, as the pattern needed to be easily reused, the `isHandeled` check got added to every condition, so it made copy and pasting much easyer for the future.

```cs
bool isHandeled = false;

if (!isHandeled && newCondition1){
    // do the other work
    isHandeled = true;
}

if (!isHandeled && condition){
    // do the initial work
    isHandeled = true;
}

if (!isHandeled && newCondition2) {
    // do completeley different work
    isHandeled = true;
}
```

Sometime, smeone, somehow, figured out that, in order to be absolutelty sure that no bug can enter the code, could use an `else` statement. But, as any coution developer that does not trust unit tests written by a fellow collegue, it simply added new code, instead of applying refactoring. 

```cs
bool isHandeled = false;

if (!isHandeled && newCondition1){
    // do the other work
    isHandeled = true;
}
else if (!isHandeled && condition){
    // do the work
    isHandeled = true;
}
else if (!isHandeled && newCondition2) {
    // do completeley different work
    isHandeled = true;
}
```

Of course, the developer added this to all the if statements in the code. (as always, for consistency reasons).

Following his scepticism, he made sure all conditions were properly written, so, when a value got tested for equality, it was tested for it's inequality also. With the AI comming to take over the planet, you can never be to cautious.

```cs
bool isHandeled = false;

if (!isHandeled && newCondition1){
    // do the other work
    isHandeled = true;
}
else if (!isHandeled && condition){
    // do the work
    isHandeled = true;
}
else if (!isHandeled && newCondition2) {
    // do completeley different work
    isHandeled = true;
}
else if (!isHandeled && someVariable == someValue) {
    // do specific work in case someVarialbe has the exact someValue value
    isHandeled = true;
}
else if (!isHandeled && someVariable != someValue) {
    // do work in your own pace, but only after you made sure you are doing it right
    isHandeled = true;
}
else if (!isHandeled) {
    // do the work that nobody else wanted
    isHandeled = true;
}
```

Now, if only `else` was powerful enough not to need that `isHandeled`, the developer thought, but, who can know that for sure?
