# The extension 

Somewhere, in a secret underground laboratory, models were build and persisted to storage devices.

There, the interface was developed. It had one method, but that's all it needed. It's codename was IBuilder, and it was internal.
```cs
interface IBuilder {
    TheModel BuildModel();
}
```

While it was not the perfect interface, it was a happy interface, knowing what it needs to say, and communicating it well enough for others to understand. (or, at least, keeping the complaints to a minimum)

It had a lot of children, a lot of classes implemented this interface. And all the classes were doing mostly the same thing, but in their very own home. They thought about it as training, preparing themselves for hard times, when they'll be fully grown and much much bigger. One of those classes was the one below.

```cs
class ModelBuilder: IBuilder {
    public TheModel BuildModel (){
        // huge piece of code that gets data from external services 
        // mostly the same in all siblings

        return theNewlyBuildModel;
    }
}
```

After a quick look, someone thought it would be better to extract the `// huge piece of code that gets data from external services` into an extension method. 

So this happend:

```cs
static class ModelBuilderExtender {
    public static T GetExternalData<T>(this IBuilder builder){
        // instantiate the appropriate service by the type of T
        return externalData;
    }
}
```

And the model builder became:

```cs
class ModelBuilder: IBuilder {
    public TheModel BuildModel (){
        this.GetExternalData<SomeSpeicificModelThanOnlyModelBuilderKnowsOf>();

        return theNewlyBuildModel;
    }
}
```

Because the new and shiny extension method was generic, there were cases when it needed to do logic dependent of the type T, and who else knew better how to deal with T than the ModelBuilder itself? 

So, the following things happened:

- Interface got a new member. It was said it protested a bit, but it was just a rumor.
```cs
interface IBuilder<T> {
    TheModel BuildModel();
    T DoSomeInternalWork();
}
```
- The builders implemented it with saddeness, but control was taken from them allready so they listened to their bosses.
```cs
class ModelBuilder: IBuilder {
    public TheModel BuildModel (){
         this.GetExternalData<SomeSpeicificModelThanOnlyModelBuilderKnowsOf>();

        return theNewlyBuildModel;
    }

    SomeSpeicificModelThanOnlyModelBuilderKnowsOf DoSomeInternalWork(){
        // doing that internal work
    }
}
```
- But the extension method was happier than ever, because now, finally, it could do it's work.
```cs
static class ModelBuilderExtender {
    public static T GetExternalData<T>(this IBuilder builder){
        // instantiate the appropriate service by the type of T
        var someResult = builder.DoSomeInternalWork();
        // transform someResult to externalData
        return externalData;
    }
}
```

Of course, all the other builders had some more work to do, so they implemented the newly created interface. The ones that did not need it, did what they knew best, they threw exceptions to express their disgust.

Things worked for a while, everyone delegated the wrong things to the wrong entities, but, hey, that's like real life, right? 

Until one day...

It was a monday morning, and the coffee was fresh. The clouds cleared the sky and the sun was shining, heating and melting everyone's brains.

Someone, flying around in it's own personal pane, looked at all those sad builders, and decided to give a helping hand by extracting a base class for them. 

Of course, the only thing that could not be moved there, was the `DoInteranlWork`. So, the ModelBuilders moved from fulltime to parttime jobs, still earning their pay.

They looked like this:
```cs
class ModelBuilder: BaseModelBuilder {

    public override 
    SomeSpeicificModelThanOnlyModelBuilderKnowsOf DoSomeInternalWork(){
        // doing that internal work
    }
}
```

And still, the extension method was happy, and the bulders, were, in their way happy, or, at least, accepted the world they lived in and got on with their lives, increasing their debts and not looking back.

Later that week, there was a ModelBuilder revolution, but it was supressed before it could even start properly. There was also an interface revolution, but nobody remembers what the outcome was.

So things kept happeing. Extension methods multiplied and got more and more powerfull, concuring and owning interfaces, and dictating things around. The pattern was simple enough to be understood by most people, so they happily applied it. Why? 

Because models got build, and that is what mattered, right?



