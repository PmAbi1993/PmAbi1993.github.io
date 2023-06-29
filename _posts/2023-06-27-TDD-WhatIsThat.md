---
title: Do you really need TDD?
date: 2023-06-27 01:00 +0000 
tags: [TDD, swift]
pin: false
---

# YES

I would say _YES_ undoubtably.

If you are not under strict tight time schedules, Then following TDD would be heavenly for your project. If you are working on a company or personal product, then the answer would again be undoubtably yes.


# What is TDD

One of the reasons I had to add an explanation is because, the nature of TDD is not visibly explanatory to most developers. It is essentially a coding style. Most developers probably wont understand if the code was written by following TDD just by looking at the code and people have came up to me asking what does this TDD mean anyway.

From what they see, It is just a lot of testcases and dependancy injection to make sure the files have 100% coverage. 😅.

True, TDD => practice that involves writing tests before writing the code. The failing ensures that both Happy path & sad path are covered.

But do you know what is the best thing about TDD that no one talks about?

> 1. Thinking before coding it in. 
> 2. Having a clear idea of what you are coding in.
> 3. Book and paper approach to get the idea in mind

Let me explain my thoughts below

# How do I do it.

This is not a benefit that is only present for TDD, but while building anything we need to have a proper understanding of the feature. It would be great if we are able to write at least a dependency diagram, algorith / contract or a UML diagram that describes what we are building.

Starting in a book and paper means you are actually invested in the thought and not thinking as we input the code. Without this coding with TDD will be harder because you would be just doing a test coverage run.

## 1) Proper Dependency injection

Since we have started from a book on paper, but we would be knowing how every object need to be composed. We would write up contracts and make the Domain layer separate and mocking data for each case and make sure every path is covered.
Can there be cases that I missed that can come up in future. Sure, that's how developement goes. You will need to add in more feature, fix bugs that could arise from paths you never foresaw and the diagrams or alogorithms you wrote will help you solve it much quicker

## 2) Covering breaking changes and behaviours rather than test coverage.

While doing TDD you will be tempted to add coverage to all code. We have to understand that getting a 100% test coverage is not the objective of TDD. The main obejctive is to write fool proff code that can be extended in teh future without breaking multiple things in the app and making sure all rule sets are followed

## 3) Documentation 😃

Nobody likes to document our code. It is an axiom 😃. I know develoeprs who would rather quit than to write documentation for the stuff we put in. Sometimes it can be a time consuming and a rather unfortunate task when the requirements keep on chaning. This is tackled by writing self documented code, But this can loose its quality over frequent re-writes under tight schedules.

But since we are working under TDD, A 3rd person can actually visit the code, understand what he can, Move to the test cases and just walk over the test cases to see what the developer was intending to cover throught he functions he has written. I have found much information through testcases than through invalid documents from some projects that I have worked on.

## 4) De-coupling of elements

When you are writing test cases for behaviours with TDD, you are inadvertantly de coupling the logic. To cover the behaviours we have to inject properties, override components and much more. To handle this you would start thinking in composable items rather than concrete obejcts.

Once you start working with contracts or blueprints of objects in mind & you have started to create proper abstractions, You have already won. The code starts to become loosely coupled and most of the time much re-usable than it could have been otherwise.

This could particualry be useful when we have to replace some components from project, and the only changes you would have to do would be in the lowest coupled concrete implentation. Once you start to use composition rather than inheritance, your project could scale to the level you want efficiently.

# So it does not have cons?

Hehe, I wish. Like everything there is a lot of things that we have to consider when we write in TDD. It has its own set of head aches.

## 1. Learning curve, implementation & maintainance overhead:

It takes times to be good in writing abstractions and implemt proper tdd. It would be hard to some perople intitially to think in terms of contracts and this can lead to rather large & improper abstractions. And even on making changes to some features, we may have to re-write a large number of test cases to make the pipeline pass. But this would be a blessing in disguise or a curse we have to live with. 😃

## 2. TDD != Unit test cases

Never exclude E2E testing just because you have test cases. We may think we have covered all cases and scenarios, but the world isn't that ideal, is it.

While building with TDD, I have seen people give much importance to unit tests and they forget the part that we have to have some integration tests to backup the real life data. The fall sense of hope that the unit test cases provide should not be your strong case.

# Should you do it?

Sure, If you have the time and patience it is better to start with TDD. 

> Starting a project in TDD would be a hassle, But maintaining one in long term would not. 

Do check with your team on how confident are they with the approach. If the project has a relatively short timeline or limited resources and the confidence with team isn't high it can backfire and you may miss deadlines.

# Bonus - Myth is MVC & TDD compatible?

Surprisingly I have had a debate with one of the develoeprs I know who said he isn't doing TDD because he is using MVC to build his apps.

The architectural pattern has no real relevance here. This would be the equivalent to saying MVC is bad because it creates massive view controllers. Improper MVC can cause large view controllers, but we have to emphasis on the word `Imporper`.

MVC code can be written with TDD too. It should not be an excuse to not write test cases 😃.

