#### Which one would you choose?

In 2007, Google's Product Manager, Dan Siroker, took a leave of absence to head the "New Media Analytics" team for the presidential campaign, of then Senator Barack Obama. He was brought in to apply Google's web practices on the bright-red DONATE button of the campaign's site. And the results: Astonishing, $57 Million of additional donation was raised, directly due to his work.

How you ask? Well, it's simple. 

He *A/B tested*, his options.

Let me explain.

As we have seen previously, and also when we were younger, again previously, there is more than one way to solve a problem. And here, more than one way of designing a website, color of the donate button, size, text, photos, videos, less, more, every variable can have a serious impact on the solution. In A/B testing, we try out a variety of different parameters, and analyze different metrics, that effectively tell us how good the web site design was. These metrics can be time spent by user, amount of money donated, page shared, etc. All the things, that can measure users interaction with the website. This way they can select the best color, combined with best text, combined with photos, etc. Did you know, that the design featuring a simple, black and white photo of the Obama family, outperformed all other photos, even videos did not come near to this photo.

Now how do you minimize, spending of capital, on searching for the best, while maximizing the returns on current best option?

Here, again you can brute force, and try every other combination equally, and then select the best. But think again.

There are 2 major flaws to this plan:

1. Is wasting **equal** amount of capital, effort and time on a later discovered bad option worth it! The key word here, is **equal**. 
2. Do you even have that much capital, effort and time to try out all options, and then have some more to actually, use the best option found!

It is worth spending some capital on bad options, because if you don't, you may pass up a golden opportunity, just because you were worried it might incur some losses. This problem is defined as the **Explore/Exploit** problem in computer science.

How do you allocate your resources to explore new - better, solutions, while exploiting your current best?

Over the course of history, many algorithms have been designed to solve this problem, namely, greedy, $$\epsilon$$-greedy, Gittin's Index, Upper Confidence Bound Interval(UCBI), etc. Here, we are looking at current best, and the simplest one, i.e. UCBI. 

It works on the same idea of error measure. It is like, when you buy any measuring instrument, say a ruler/scale, it may measure 1 cm as 1.01 cm to 0.09 cm (i.e. $$\pm$$ .01 cm). this .01 cm is called the error. So, whenever you record your results, with the use of this ruler you will write it like $$1 \pm .01 cm$$. 

So, for simplicity sake, let's say, you have 4 designs, which wanna explore, and exploit the best of them. So, in the start, you assign an equal error measure and metric scores to all the 4 options, and randomly pick one design. Get the metrics for it.

After this you get some information about the design selected, which makes the uncertainty or the error in your decision, a wee bit small. So, over time, as you explore and get more information for each design, the $$\pm$$ error in your decision is going to decrease in your decision, which will help you make better informed choices. 

So, the formula for this goes, in a very rough sense like,

$$Exploitation \hspace1mm Chance \hspace2mm =\hspace2mm  Metrics \hspace2mm + \hspace2mm Error \hspace1mm Interval$$

![UCBI.png](/blog/assets/img/UCBI.png)

Here, for our next action, we choose A. We see that, even though the design 'C' has more metric score, and less error interval, design 'A' hasn't been explored the same to make an informed decision. In fact, there is a probability that, it will payout more than 'C', because it's upper error bound is higher. In this case, design 'B' will probably not be further explored, because it can never outperform 'C'. It's upper bound is lower than 'C'.

Every time, we choose the design with the highest upper bound. This increases our chances of getting best results, with spending the least amount of money.

This type of exploration/exploitation problem exists in our daily lives on a small scale, like choosing which restaurant to visit, which movie to watch this weekend, whom to hangout with, etc., to large scale like, optimal design for shoe, website, best treatment selection, etc.

Internet has now become the largest controlled experiment. And what are these companies experimenting? Whatever it takes, to make you move your mouse, and open your wallet. 

> The best minds of my generation are thinking about how to make people click ads. It sucks.
— Jeff Hammerbacher

Another problem, that is based on explore/exploit, is clinical trials. Traditionally, you divide the patients randomly in equal 2 groups and treat one with maybe placebo (or current best treatment), and other with new treatment. Here, we allocate equal resources to both groups, i.e. equal number of people in both groups. 

Millions of dollars are at stake in an experiment to find the optimal configuration of a website, but in clinical trials, experimenting to find optimal treatments has direct life-or-death consequences. Many doctors and statistician and I too, think this the method used is wrong. Computer Science has figured out optimal way of finding best treatment, why let 50% of people, get less optimal treatment. 

More about this in next blog, for now, face uncertainty with optimism, and don't be afraid to try out new things. You are anyways going to regret some of your decisions anyway. You can minimize your regret, by exploiting the best possible option, but also regret not getting to know other way, so keep exploring! ✌🏻

---

Reference: Algorithms to live by — Brian Christian and Tom Griffiths
