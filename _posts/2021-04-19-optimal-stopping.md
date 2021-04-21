---
title: "Knowing when to stop"
date: "2021-04-19"
categories: book algorithms-to-live-by
---
In life, everyone tells us to never give up on our dreams, you never know how close you are. And you should not give up, but only some of the times. Many people apply this strategy everywhere. Look for the best job, best offer, best partner, best house, best, best and best. No one ever tells us when to stop looking.

Let's say for example, you want to hire an assistant. You have 100 applicants for the position, and it is a immediate hire. And once you have passed over the opportunity to hire the applicant, you cannot recall him/her back. You have no quantifiable information about the applicant. You can only rank the applicants relatively, using ordinal values.

Here, you have different methods with which you can hire

1. Hire at Random
2. Hire the best yet
3. Hire the second best yet

At random, you have 1% chance of hiring the best. If you go with the best yet, well 1st one is best yet 😎, and again there's a 1% chance that he/she is the best. If you go for second best, you are already not fighting for the best. Now, you may say that you have to look for sometime and then hire the best. There's balance. Okay I agree, but how much time, or how many applicants before committing for the best yet? Well, mathematicians have already solved this problem. The problem is of **optimal stopping point**. 

So, here the simple rule is like previously stated, **Look-Then-Leap** rule. How much time to look? **37%**. So, if you wanted to hire the best assistant possible, you have to non-committedly interview 37 of the applicants and then immediately hire the best one yet after 37th. This gives you the 37% chance of hiring the best, though not a guarantee, still much better than 1% 

Let's move on to the interesting part, where we solve it using examples. 

- Say you only have 1 applicant. You hire immediately
- 2 applicants. You have a 50% chance of hiring at random. Pick any of the 2.
- Now here's where trickery begins. Now you have 3 applicants, which one do you hire? At random you have 33% chance of hiring the best. There are 6 permutations of ranking applicants relatively.{(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)}. Here if you select the first candidate, you have a 33% chance of selecting the best. But if you hire the best yet after first (33.33%), you select the best one 50% of the time.


| Number of applicants | Applicants to Skip | Chance of getting best |
|---|---|---|
| 3    | 1 (33.33%)  | 50%
| 4    | 1 (25%)     | 45.83%|
| 5    | 2 (40%)     | 43.33%|
| 6    | 2 (33.33%)  | 42.78%|
| 7    | 2 (28.57%)  | 41.97%|
| 8    | 3 (37.5%)   | 40.97%|
| 9    | 3 (33.33%)  | 40.59%|
| 10   | 3 (30%)     | 39.87%|
| 20   | 7 (35%)     | 38.42%|
| 30   | 11 (36.67%) | 37.86%|
| 40   | 15 (37.5%)  | 37.57%|
| 50   | 18 (36%)    | 37.43%|
| 100  | 37 (37%)    | 37.10%|
| 1000 | 369 (36.9%) | 36.81%|

Now obviously this will never be a direct real world scenario, but just like we have variations to the main theory in chess, we have variations to the optimal stopping problem too. In the above case, we had no information about the applicants. We only, knew which one is better, but not by how much. Now let's say you wanna hire a typist, with the maximum typing speed. Here, you just look at typing speed and nothing else. This is an example of full information and here you do not wait before hiring the best yet. Here you apply, the **Threshold rule**. Say for example, anything above 90th percentile is the threshold. 

But again, it matters with how many people you have left in the pool. For this let's start backwards. You are at the last person and there's 0 applicants left. Now you have to hire, no option. But say second-last, here you look if the score is above 50 percentile, if yes you hire, else give hire the last, because they both have 50% chance of being the best. 3rd-last, if score is above 67 percentile you hire. 4th-last, 75. 5th-last 80. The chance of ending up with the best applicant in the pool, in this full information scenario, is 58%. Much better 37% in no information.

There is another variation, recall. Say you don't have to necessarily hire immediately, there's a 50% chance the applicant will join, if recalled. Another variation is rejection. Say the applicant rejects the given offer.

This can be applied to any measurable range metric. Time, applicant ranking, parking spots to consider, etc. For example with time, you look for 37% for the time and then leap at the best opportunity. Another variation is cost of looking, in most cases it is time, but for example, in selling suppose a house, the property tax is monetary cost. 

This works in many cases ranging from , who to hire, when to sell, where to park, to whom to marry, when to quit. It basically, is when to change the current action for maximum profit.

> Though all Christians start a wedding invitation by solemnly declaring their marriage is due to special Diving arrangement, I, as a philosopher would like to talk in greater detail about this ...
-- Johannes Kepler

<span style="background-color: #FFFF00">[Interesting Fact]</span>: Research shows that, when a group of people where challenged with the same problem, they looked non-committedly for about 31% of the time. Now in this example, we didn't consider the cost of time, time went into interviewing, time without assistant. If we factor this in, we get to approximately 31% of looking. So by evolution or some Divine intervention, we instinctively look for 31% of the time, applicants, etc.
