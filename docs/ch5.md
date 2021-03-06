# 第 5 章 实体

> Chapter 5. Entities

I’m Chevy Chase . . . and you’re not.

—Chevy Chase

There is a tendency for developers to focus on data rather than the domain. This can happen with those new to DDD, because of the prevailing approaches to software development that place importance on the database. Instead of designing domain concepts with rich behaviors, we might think primarily about the attributes (columns) and associations (foreign keys) of the data. Doing so reflects the data model into object counterparts, which leads to almost every concept in our “domain model” being coded as an Entity abounding with getter and setter methods. It’s easy to find tools that will generate all that for us. Although there may be nothing wrong with property accessors, that’s not the only behavior DDD Entities should have.

It’s a trap that was sprung on SaaSOvation developers. Learn from their lessons in Entity design.

Road Map to This Chapter

- Consider why Entities have their proper place when we need to model unique things.
- See how unique identities may be generated for Entities.
- Look in on a design session as a team captures its Ubiquitous Language (1) in Entity design.
- Learn how you can express Entity roles and responsibilities.
- See examples of how Entities can be validated and how to persist them to storage.

## WHY WE USE ENTITIES
We design a domain concept as an Entity when we care about its individuality, when distinguishing it from all other objects in a system is a mandatory constraint. An Entity is a unique thing and is capable of being changed continuously over a long period of time. Changes may be so extensive that the object might seem much different from what it once was. Yet, it is the same object by identity.

As the object changes, we may be interested in tracking when, how, and by whom changes were made. Or we might be satisfied that its current form implies enough about its previous state transitions that explicit change tracking is unnecessary. Even if we don’t decide to track every detail of its change history, we could still reason on and discuss the sequences of valid changes that could occur to these objects over their entire lifetime. It is the unique identity and mutability characteristics that set Entities apart from Value Objects (6).

There are times when an Entity is not the appropriate modeling tool to reach for. Misappropriated use happens far more often than many are aware. Often a concept should be modeled as a Value. If this is a disagreeable notion, it might be that DDD doesn’t fit your business needs. It is quite possible that a CRUD-based system would be more fitting. If so, that decision should save your project both time and money. The problem is that pursuing CRUD-based alternatives doesn’t always save those precious resources.

Businesses regularly put too much effort into developing glorified database table editors. Without the correct tool selection, CRUD-based solutions treated elaborately are too expensive. When CRUD makes sense, languages and frameworks such as Groovy and Grails, Ruby on Rails, and the like make the most sense. If the choice is correct, it should save time and money.

Cowboy Logic

AJ: “What kinda CRUD did I just land in?”

LB: “That’s a cow pie, J!”

AJ: “I know what pie is. You got your apple pie and your cherry pie. This ain’t no pie.”

LB: “Like they say, ‘Never kick a cow pie on a hot day.’ It’s a good thing you didn’t kick it.”

![](cowboy_logic_conversation.jpg)

On the other hand, if we apply CRUD to the wrong systems—more complex ones that deserve the precision of DDD—we may regret it. When complexity grows, we experience the limitation of poor tool selection. CRUD systems can’t produce a refined business model by only capturing data.

If DDD is a justifiable investment in the business’s bottom line, we use Entities as intended.

When an object is distinguished by its identity, rather than its attributes, make this primary to its definition in the model. Keep the class definition simple and focused on life cycle continuity and identity. Define a means of distinguishing each object regardless of its form or history. . . . The model must define what it means to be the same thing. [Evans, p. 92]

This chapter teaches how to place the proper emphasis on Entities and shows you various Entity design techniques.