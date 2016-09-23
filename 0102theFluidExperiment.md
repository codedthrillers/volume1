# The fluid experiment

There was a time, when everything was solid. And then, there was a time, when everything was fluid. When these times passed, a new era came, when all things got vaporous, but we are not concerned with that.

This story takes place in the transition years, around the time `IfValid` was born.

```cs
public static T IfValid<T>(this T objectToValidate){
    if (StaticGenericValidator.validate(objectToValidate)){
        return objectToValidate;
    } else {
        return null;
    }
}
```

As all main protagonists, the `IfValid` had its flaws. It knew about them, and hid them as good as it could.

It looked at itself and tried to find find its purpose in life. The only one it could think of was this:
```cs
someObject.IfValid()?.CallMethod()
```
Not too great, but not too small either. `IfValid` accepted it.

Meanwhile, developers were trying to get rid of the static class reference, the so called `StaticGenericValidator`. They all agreed that using static classes was smelly and, they were looking for a perfume to hide it. And then, `IfValid` burst into existence. It was such a perfume, a breath of fresh air, the smell of pine trees and clean water.

Developers were so content with it, that they sprayed it everywhere. 

So this happened, all over the codebase, making `IfValid` feel almighty and powerful:
```cs
if (object.IfValid() != null) {
    // do stuff
}
```

Until one day, someone argued `IfValid` was not easy to read, so he decided to apply `extract variable` technique. 

And it became more expressive:

```cs
var isValid = object.IfValid() != null;

if (isValid){
    // do stuff
}
```

And, it seemed to be readable enough, so they sprayed this new perfume over the other (this one smelled like peaches).

The `IfValid` method started to doubt itself, and passed through a confidence crisis. It cried for help, but nobody heard it. It wanted back between the brackets.

A new developer came. He hated peaches, so decided to clean the air. So, putting on the creator hat, he gave `IfValid` a sibling. It was called `IsValid`, and looked like this:

```cs
public static IsValid(this objectToValidate){
    return objectToValidate.IfValid() !== null;
}
```

Little did he know, that this not only depend the `IfValid`'s confidence problem, but threw it in depression. It's only purpose was to be used by its brother, IsValid. It even started to envy `StaticGenericValidator`.

After days of useless therapy, `IfValid` suddenly found a friend.

It was late in the evening, and everybody was tired. Fingers mingled on the keyboards, and characters where overlapping. This is how `IfValid` met *TheTypo*. 

They quickly became friends. `IfValid` started regaining it's territory, making some order in the chaos that IsValid created.

Weeks have passed, and things finally got balanced. Most of the work was still done by IsValid, but `IfValid` got it's share of usages. 

As solid became fluid, IsValid quickly became forgotten, and `IfValid` favored again. And, although fluids are slippery, and are hard to contain in porous recipients, it cringed to everything it could, reinventing itself, and finding new purposes. Like this:

```cs
 var result = oneObject.IfValid()?GetData()?.IfValid().Result;

 if (result != null){
    // do stuff with result 
 }
```

*If only, `Result` could be validated*, `IfValid` thought.

One time, a junior developer came, and found this construct interesting. She studied it, learned from it, ... and made a `Result` validator.

She then knew how to create fluid interfaces. 

And then things started to boil...
