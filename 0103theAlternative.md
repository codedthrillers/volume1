# The Alternative
*(or how to write boolet proof code when no bullets are flying around)*

There was an `if` and it evaluating it's condition.

```cs
if (condition){
    // do the work 
}
```

And somebody wanted to do something else, if the condition was not satisfied. So, he needed a way of knowing if the `if` block was executed or not.

And, as it was deep in the night (the time monsters appear), this tiny dragon was born:

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

Unit tests were written, and the behaviour was as expected. The problem was with the requirements. They grew. (and so did the baby dragon). 

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

Everything was fine. The allready proven working pattern could be now used by others.

The dragon was given wings:

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

One day, the conditions needed to be reordered and, as the pattern needed to be easily reused, the `isHandeled` check got added to every condition. This made copy and pasting much easyer for the future. And this is what mattered.

The dragon flew into the night, and roamed silently above the city:

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

Sometime, someone, somehow, figured out that, in order to be absolutelty sure that no bug can enter the code, could use an `else` statement. But, as any coution developer that does not trust unit tests written by a fellow collegue, it simply added new code, and wrote it's own tests. He then added this to all other `if` statements. (Why? for consistency reasons, of course). 

The dragon roared, and roared, and roared: 

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

... and finally someone heard it, and got scared.

He rushed to the keyboard, made sure all conditions were properly written. Each and every condition had to be perfect by now, and, just to be extra careful, when a value got tested for equality, it was tested for it's inequality also. With the AI rising from the ground and trying to take over the world, and the dragon circling the skies, you can never be to cautious.

And the dragon blew fire:

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

And everything burned.

*Now, if only `else` was powerful enough not to need that `isHandeled`,* the developer thought, *but, who could knew that for sure?*
