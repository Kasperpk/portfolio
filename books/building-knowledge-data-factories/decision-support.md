Some people might resonate with the rather exhausted feeling coming home from a long day with little energy to spare. The exact root cause for this might not be obvious but as a mental exercise i would like you to go through a regular day and try to count the number of decisions you make. 

What trousers should i put on, what t-shirt would fit well with it? and what shoes should i pair with it? Should i eat breakfast at home or at my work? Do i get to work by bus, car or bicycle? Do i turn left here or at the next corner? 

Perhaps just a few minutes into a regular day you may realize that you already faced the first 10-20 or even 100 decisions depending on how little you are prepared or how many kids you have. 
The saying that we make 30.000 decisions everyday. Inspecting just at a very surface level what a regular morning might look like, the number might not be out of proportion. 

Now you might think? so what. Many of these decisions are so small and innocent and may not even really register in the conscious mind. However now imagine a day where every thing was decided for you. What to do, what to eat, how to get to work. That mental exercise might make you realize how small decisions accumulating over the day which could be a major contributing factor to feeling exhausted at the end of a day. 

This is not a self-help book however i wanted to share this which might motivate you to reduce the number of decisions you have to make on a daily basis, leaving more energy for the important work you have to do. 

The aim of this section is to understand decision making at a deep level so that we can understand the role of information therein. However it might also be motivating to know that how much it actually is a part of our personal and professional lives. 

## The scientific study of decisions

With the goal to understand decision making in-depth we will be looking at the mental process of making decisions through the scientific angle of *Decision Theory*. We might say that decisions theory is formalization of common sense that we all try to muster when we make decisions. More particularly the theory of decisions applies mathematical and psychological ideas to help us understand what dictates how an *agent* or group of agents makes a choice from a set of alternatives. Where a choice from a set of alternatives is the definition of a decision. 

Decisions could be around what we should believe, say and do. For example how much money we should gift, which seller to believe or how to tell our mom we damaged her car when trying to park it. 

To describe a decision problem, decision theory makes some assumptions. It assumes that we have a set of available actions $A$. That there is a set of states $S$ of which the *true nature of the world might be*. It might be that your Mom is angry, disappointed or even glad it didn't end up worse. Finally the decision maker is assumed to have some idea of what the consequences or outcome of each action will be in the different states. So if your Mom is very touchy about her car you probably know that you have to tell it to her it the right moment and use the right words. So there is some form of measure which is called *utility*. On the other hand the Mom has to *choose* her reaction based on her own values and preferences.  

Utility is a subjective numerical measure and is interesting because it measures everything in the psychology of the decision maker. It can be difficult to put a number to the utility you would gain or lose by saying, believing or doing things in a certain way, but in order to define the problem and use mathematical operations this measure is needed. 

Consider for example entering a gamble where you can win $120 if a fair coin turns tails and lose $100 otherwise. We can solve the pure mathematical expected value given these data. By computing the probability $p$ of being in a certain state times the payoff in that state. 

So we have the following states of nature 
* $\theta_1$ The coin turns out tails
* $\theta_2$ The coin turns out heads 

You have the following actions $a_1$ : enter the gamble or $a_2$ don't enter the gamble. Let's assume for a moment that all you care about is the pure mathematical expected value. Then you might calculate the utility from the expected payoff for each action and state of nature. 

The payoff will be 120 if you are in the gamble and the coin turns out tails. If it instead turns out heads the payoff is -100. If it instead you choose not to gamble the payoff will be 0 no matter what the state of nature is. We can summarize it in this table.

| $U(\theta, a)$ | $a_1$ | $a_2$ | $w$         |
| -------------- | ----- | ----- | ----------- |
| $\theta_1$     | 120   | 0     | $\frac 1 2$ |
| $\theta_2$     | -100  | 0     | $\frac 1 2$ |
We have a fair coin so we know that the probability of each state of nature is $\frac 1 2$. We might call this the *a prior* probability, which i will explain more deeply later. 

So now we can calculate the weighted average utility of each choice given the *a priori* probabilities. We use the following formula which sums up the weighted utility for $a_1$ $U(a_1) = w \times U(\theta_1, a_1) + (1-w) \times U(\theta_2, a_2)$ 

$U(a_1)$  $0.5 \times 120 + 0.5 \times -100 = 10$ 

$U(a_2)$  $0.5 \times 0 + 0.5 \times 0 = 0$ 

So it would seem that the best choice, that which maximizes utility is to enter the gamble as $10 > 0$.  We might think this would be an obvious choice however human psychology might shift the utility in favor of avoiding losses. The famous experiments by Daniel Kahneman and Amos Tversky showed that people are typically risk-averse when it comes to gains but risk-seeking when it comes to losses, and that a loss hurts roughly twice as much as an equal gain pleases. 

Different factors come in to play. For example if the gamble is presented a kid who just saved up their first $100 and only has those money to spend on weekend candy and entertainment. This would likely make the loss hurt even more. It's similar to how incline someone would be in taking a very obvious positive expected value gamble such as winning $1.000.000 versus losing only $500.000. If the person just saved up $500.000 versus one with $5.000.000 then there is more to lose for the first person which decreases the utility of taking the gamble. The million is not worth as much (in utility) as it would cost in lost utility of going back to 0. 

This means for example that the loss is accounted much higher and instead of the original loss of 100 in dollar terms the utility lost might be 200 or more

| $U(\theta, a)$ | $a_1$ | $a_2$ | $w$         |
| -------------- | ----- | ----- | ----------- |
| $\theta_1$     | 120   | 0     | $\frac 1 2$ |
| $\theta_2$     | -200  | 0     | $\frac 1 2$ |
When you now calculate the utility of each action it becomes evident why a no gamble might be the choice. 

$U(a_1)$  $0.5 \times 120 + 0.5 \times -200 = -40$ 

$U(a_2)$  $0.5 \times 0 + 0.5 \times 0 = 0$ 

One might argue how "rational" those preferences or utilities are. But in general it's useful to say that "preferences can't be irrational" instead a choice can be irrational if it does not optimize the utility. 

There are different types of decisions which changes the problem and ways of solving it. In the decision above there is uncertainty due to *randomness* introduced by the coin flip. However in many practical decision problems we uncertainty is due to *ignorance of the true state of the world*. Instead of knowing the exact probability distribution of the states, we have to somehow make a guess by making our *priors* from the best information and data we can collect. 

This is the type of uncertainty we will try to study and hopefully see how high quality information can help make uncertainty into randomness or even closer to certainty and *perfect information*. An example of a decision under certainty could be the choice between an unconditional cash grant of $1.000 versus $500. If we have perfect information like this we don't really have a decision problem.

In addition to certainty, randomness and uncertainty there are also decision problems which are corporative or multi-agent. For example and Mom and son situation introduced this interactivity of decisions which also has it's own name and branch of study called *Game theory*. I will not dive much into this because much of the same concepts exists. 

In business many decisions are both interactive and complex in that they can have widespread effects and consequences. Managers for example have to consider the effect of their decisions on future customers, brand and the ability to stay in the market. For example what price to set? What marketing campaign to launch? 

In addition to making decisions in very complex and widespread effect of decisions. These decisions also can have multiple objectives which to try and optimize such as cost, quality and speed. These might be competing and difficult to make measures around. Because how much would you be willing to pay for another "unit" of quality or speed. Multiple objectives are also part of life decisions such as choosing what car to buy. There are likely multiple objectives you are trying to balance such as price, size, range, brand and so on. To solve these problems we would have to measure and weight these quantities. For example how much utility does lower price versus range provide? and is there diminishing returns on any of the dimensions? Decision like these are so complex that we often have to make *models* and that is what decision theory tries to do. It also might be the reason we can feel extra exhausted if we are in a phase where we consider a new house and might end up at some point just picking one when decision fatigue gets to high.
## Information in decisions
We have seen some very simple decisions, one under risk based on a known probability distribution of a random variable such as the toss of a coin. Knowing the frequency with which a coin is expected to land enables us to use that as *a priori* and calculate the expected payoff and utility for the outcomes dependent on that variable. In essence the knowledge of the probability distribution of a coin is *data* and information that is useful. Because imagine you enter the gamble without any sense or idea of the likelihood of the states of nature, then you are left completely to your own devices. You might look at the thing, the coin and make a reasonable guess. For example it has a symmetric shape would lead one to believe that it's equally likely to land on either side. 

That is how most decisions are made. Where uncertainty is because we are *ignorant* and don't have enough *information* to understand the randomness involved.

To make a more realistic example you might consider a decision like going to work by car or by bus. What is uncertain about this decision is that depending on the traffic you find that one option is usually better than the other. If there is a lot of traffic, the bus usually is able to get around faster since it has it's own priority lane. If there is medium or low traffic the car usually gets there faster since it rides without unnecessary stops and with greater speed. 

So we have three states of nature.

$\theta_1$ : Traffic
$\theta_2$ : M Traffic
$\theta_3$ : Traffic

We have the two actions $a_1$ take the bus and $a_2$ take the car. To complete the decision problem you make some quantifiable measure of the utility you experience in the combinations of states of nature and actions. 

| $U(\theta, a)$ | $a_1$ | $a_2$ |
| -------------- | ----- | ----- |
| $\theta_1$     | $-1$  | $-6$  |
| $\theta_2$     | $-3$  | $-3$  |
| $\theta_3$     | $-5$  | $-1$  |
Assuming that you would rather not have to commute at all the utilities are negative. Without knowing what the traffic is going to be like the actor will end up sometimes sitting in the car wishing he took the bus or sitting in the bus wishing he took the car. One cautious way to solve the decision problem is to look at the worst that can happen. Taking the bus can at most cost 5 while taking the car can cost 6 utility, so the bus limits the damage. Decision theorists call this the *minimax* rule. It is deliberately conservative and pessimistic since it only asks how bad things can get and ignores how likely that is. 

To do better than that the decision maker may try to figure out what kind of data and information can reveal or indicate what the state of nature is. As humans we are quite intuitively trying to understand patterns so that we can predict. However our intuition, the fast thinking that Kahneman calls *system 1 thinking* can also strongly fool us.  

What could be a piece of information that could indicate what the state of nature is? Perhaps particular days of the week will have some indication. Maybe Mondays tend to have heavier traffic than Thursdays or Fridays. So we can say we have observations $z_1$ : it's Monday, Tuesday or Wednesday or $z_2$ : It's not M,T,W.

Given it's Monday to Wednesday you find that 7 out of 10 days are heavy traffic 2 out of 10 have medium traffic and 1 out of 1 days have low traffic. At the end of the week you find that 4 out of 10 days have high traffic, 3 out of 10 days have medium traffic and 3 out of 10 days have low traffic. So we now have some data and we can plot that into the model as conditional probabilities of observing the data $z$ in the states of nature. 

| $P(z \mid \theta)$ | $z_1$          | $z_2$          |
| ------------------ | -------------- | -------------- |
| $\theta_1$         | $\frac 7 {10}$ | $\frac 3 {10}$ |
| $\theta_2$         | $\frac 4 {10}$ | $\frac 6 {10}$ |
| $\theta_3$         | $\frac 2 {10}$ | $\frac 8 {10}$ |
Notice the direction of this table. It tells us how often each observation shows up *given* the true state of nature, not how likely each state is given the observation. It is tempting to read the 0.7 as "if it's early on the week there is a 70% chance of heavy traffic", but that is a different number and we get to it when we reach Bayes' theorem. So when we have uncertainty we have to form beliefs based on information and that is the Bayesian way i will explain more in-depth later. 

It's possible to create a *strategy* which is a fixed rule made in advance that says which action to take for every observation that can be made. In essence you can define all the possible combinations. For example a strategy is to choose $a_1$ if you observe $z_1$ and $a_2$ if you observe $z_2$. This strategy can written as $s = (a_1, a_2)$, where the position in the tuple corresponds to the observation. 

Let's call this strategy $s_1$. 

Now let's calculate the average loss of this strategy for each state of nature. We weigh the loss of each action by the probability that the strategy ends up taking it, see equation 1.1. 

Equation 1.1 Average loss of a strategy
$$L(\theta, s) = \sum_k P(z_k \mid \theta) \ l(\theta, s(z_k))$$
If the true state of nature is that there is high traffic, that is $\theta_1$. Then there is 70% chance of observing $z_1$. 

$L(\theta_1, s_1) = 0.7 \times -1 + 0.3 \times -6 = -2.5$ 
$L(\theta_2, s_1) = 0.4 \times -3 + 0.6 \times -3 = -3$ 
$L(\theta_3, s_1) = 0.2 \times -5 + 0.8 \times -1 = -1.8$ 

So this strategy has the following losses of utility given the possible states of nature. It's the strategy that says "if it's early on in the week, take the bus else take the car" and in generally this seems reasonable given what the data is saying. A contrarian strategy would be $s_2 = (a_2, a_1)$. We can calculate the average loss of strategy $s_2$ as. 

$L(\theta_1, s_2) = 0.7 \times -6 + 0.3 \times -1 = -6.53$ 
$L(\theta_2, s_2) = 0.4 \times -3 + 0.6 \times -3 = -3$ 
$L(\theta_3, s_2) = 0.2 \times -1 + 0.8 \times -5 = -4.2$ 

In addition to these two strategies we also have the ones which picks $a_1$ or $a_2$ no matter what. In essence these are the strategies that don't even look at the data in this case, the day of the week. Let's for good matter list up the losses of those strategies. Which we call $s_3$ and $s_4$ 

$L(\theta_3, s_3) = 1 \times -1 + 0 \times -6 = -1$ 
$L(\theta_2, s_3) = 1 \times -3 + 0 \times -3 = -3$ 
$L(\theta_3, s_3) = 1 \times -5 + 0 \times -1 = -5$ 

$L(\theta_3, s_4) = 0 \times -1 + 1 \times -6 = -6$ 
$L(\theta_2, s_4) = 0 \times -3 + 1 \times -3 = -3$ 
$L(\theta_3, s_4) = 0 \times -5 + 1 \times -1 = -1$ 

This example is kept rather simple so the number of strategies are four resulting from the observation and action space $m^n$. That means if the observation and action space increases the number of strategies rise exponentially. 

There are different ways to now solve this problem. A very conservative strategy is to choose the one which has the lowest maximum average loss. That would be strategy $s_1$ since it has a maximum loss of 2.5. Another strategy is to choose the one that has the best possible outcome. Then that would be $s_3$ since that ensures that we at least sometimes choose the right transportation method. What's apparent is that $s_2$ or $s_4$ would never be chosen under any of these conditions. For example it's clear that $s_1$ is better than or equally good in all states of nature. When this is the case we say that $s_1$ *dominates* $s_2$ because no matter what the state of the world is, the average loss of utility is lower. Similarly $s_3$ is better than or equal to $s_4$ in all states of nature. 

Instead we can reduce the available strategies or we should do so to the ones which are *admissible*,that is they are not dominated. In this case every strategy but $s_2$ are admissible. 

The conservative (minimize loss) or optimistic (maximize gain) are not really by themselves reasonable. Instead we would like to have more information or at least make some sort of guess about the frequency of the states of nature. Is the very often that traffic is high or is it mostly evenly distributed? In this case we might assume that the distribution is equal so we make a *a priori* assumption from our best available information. That information allows us to calculate the average loss of utility for the strategies. With equal weights of $\frac 1 3$ we get. 

That would yield. for 

$s_1$:  $\frac 1 3 \times -2,5 + \frac 1 3 \times -3 + \frac 1 3 \times -1.8 = -0.833 -1 - 0.6 = -2.433$ 
$s_3$ : $\frac 1 3 \times -1 + \frac 1 3 \times -3 + \frac 1 3 \times -5 = -0.33 - 1 - 1.66 = -2.99$ 

With this assumption we get a clear answer to the decision problem which is to choose according to the rules of $s_1$. However this relies on the assumption that each of these states are equally distributed and in the absence of good knowledge about this decisions are generally really difficult. This is what makes it difficult but we can also get a sense now why it is that information plays a key role in decision making and the outcomes thereof. Because imagine we had a crystal ball which would tell us exactly how the traffic would be and it would still be roughly equally distributed then we could get down to the following utility.

 $\frac 1 3 \times -1 + \frac 1 3 \times -3 + \frac 1 3 \times -1 = -0.33 -1 - 0.33 = -1.66$ 

This is a quite large decrease in loss of utility which is essentially reflects the gap between the current information and perfect information. 






## Dealing with uncertainty

In the previous example i introduced a simple decision with two alternatives and three possible states of nature. We saw how to formalize such a problem such as deciding which vehicle to take to work. The formal definition of the problem required us to take some assumptions and make a *model* for the problem. We assumed the a set of states of nature, a set of possible actions and the outcomes of corresponding with the actions and states of nature. 

From those few assumptions we could make a choice based for example on the conservative minmax loss or take the action with highest possible utility. We might also be able to better read of the best decision by having put some thought to the decision problem we are facing. However the rules of pessimistic or optimistic might let you to believe that playing the lottery is wise or to never take any chances. 

Without more information most decision under uncertainty are difficult. So what we did was to introduce information. Particularly we introduced what in Bayesian terms would be called *a priori* probabilities. Additional information which might help indicate the true state of nature then updates the prior belief into what's called *a posterior* probabilities. This is idea that we update our beliefs in light of new information is an important concept when it comes to decision making and understanding the role of information. Equation 1.3 shows this show how we calculated that. 

Equation 1.3 Bayes' Theorem for belief revision
$$P(\theta_{j} \mid z_{k}) = \frac{P(z_{k} \mid \theta_{j}) \times P(\theta_{j})}{P(z_{k})}$$
Where:

- $P(\theta_j \mid z_k)$ (The Posterior Probability): The updated probability of the state of nature $\theta_{j}$ _after_ observing the data $z_{k}$. 
- $P(\theta_j)$ (The Prior Probability): The agent's baseline belief about the state of nature _before_ receiving the new data (derived from historical odds, past experiences, or baseline models).
- $P(z_k \mid \theta_j)$ (The Likelihood): The probability that this specific data signal $z_{k}$ would appear, assuming that $\theta_{j}$ is the true state of nature. This is exactly a row of the likelihood table from the traffic example, and it measures the _reliability_ or _noise_ of your data source.
- $P(z_k)$ (The Marginal Likelihood): The total probability of observing the signal $z_{k}$ across all possible states, serving as a normalizing constant.

We used the posterior to find the best action which we call the Bayes action and the loss of that action might be called the Bayes risk. So in sum this gives an idea of how a decision agent can reduce uncertainty. By creating for himself experiments and observations that generate data that can indicate the true state of nature and update beliefs allows for making a choice which is more optimal in terms of utility. By having the memory of our brain or storing data digitally the posterior from today can become the prior for tomorrow. We might also call this learning. By for example educating yourself a bit on nutrition, it may change your belief on what should be on your plate for lunch. You might put a higher probability that clean proteins and vegetables should be on your plate to get the best utility. Our brains are doing all this mathematics in our head trying to understand the world as it is and the causes and effects of certain behaviors. Purposeful information can be a serious asset in these situations which we find ourselves in very frequently. 

This way of thinking and building reasoning is very much like science. For example when light was first discovered we thought about it in one way, but as new information came along new beliefs formed as experiments by scientist revealed new things which moved our understanding supposedly towards the true state of nature. Sometimes these findings are breakthroughs and can be called new *paradigms*. The priors are what we currently believe to be true and through a scientific process of testing our current beliefs by making new experiments and seeking new information we can generate or collect data which might support existing beliefs or change the way we think and therefore behave. 


## The value of information

The previous examples have indicated how information creates value. We saw how information was able to reduce the loss of utility for the person who decides between the type of vehicle to get to work. The value came through revealing some sort of indication about the state of nature. Knowing that the day of the week can be an indicator of the amount of traffic was used to update the belief and probabilities thereby choosing a decisions which seems to yield more utility  happen. the actor can improve their utility over time. In the area of decision theory there is a related Information value theory which tries to quantify how much decision-agents in theory *should* be willing to pay for new data before making a choice. That is fundamentally what we try to understand and argue for in this part of the book. According to this theory it requires us to know a couple of things. 

1. The expected loss with the current information, which is the Bayes risk of the best action without data from equation.
2. The expected loss we would achieve with the new data, and the cost of obtaining it. 

For example what would the person pay to know exactly if the traffic was heavy, medium or low on a given day? We saw that the loss of utility with the observation of the given day in the week and a general distribution of the states of nature was -2.433. This could be reduced to -1.66 in case that he could know what the state of nature was in that day. The difference of 0,773 units of utility is essentially what the actor would be willing to pay for obtaining that data. So whatever that translate to in dollar amounts is the price the person is willing to pay. 

In general we can say that the more the data and information can improve the utility the more value it brings. Calculating that value is like any other part of the model based on assumptions of the utilities, states of nature, actions and how well the proposed or suggested data would be able to indicate what the right thing to do is. We might call it the expected value of sampling information since it's typically that situation which decision makers are facing. For example you might have to figure out if it's worth spending time calling a colleague or looking up a news page to find out more about the state of the traffic that day. If that has enough information value compared to the cost it would be valuable to collect that information. 

Equation 1.5 Expected value with sample information
$$EV_{WSI} = \sum_{k} P(z_{k}) \times \max_{i} \left[ \sum_{j} P(\theta_{j} \mid z_{k}) \times u(a_{i}, \theta_{j}) \right]$$
This has profound implications to the work of a data professional. This analysis of the role of information in decision helps make it clear what the role of the data professional and the data science discipline in businesses are in general. In that way it can help transform our work from simply moving and transforming data to something more concrete and tangible. It's no longer a technical exercise but instead a concretely about collecting and providing access to information. But not any kind of information. The information which reduces the gap between the utility gained with perfect information about the true state of the world and what it's currently available. This position is useful because it orient us towards the decision problems and how to solve those rather than thinking about it as a technical exercise. The work of a data professional can also be expressed Bayesian terms. The data that is collected ad-hoc or on a continuous basis can if fit for purpose update the beliefs of the organizational agents and through *a posteriors* yield higher utility. 

Approaching our work from this angle also helps us understand the importance of having data which is fit for purpose. In other words data which is of high quality. Low data quality is both bad in the sense that it can lead to reduced utility or it might even lead the decision maker in the wrong direction. This means it amplifies the losses of utility instead. Data quality has several dimensions which we will look into later. For example timeliness is one of those dimensions. Stale or delayed data means that the the prior $P(\theta)$ is not updated to the *a posterior*. 

As data professionals we have to be the ones that care about these issues. By understanding the role of information in decisions we see and understand that our role can be immensely useful and help organizations deal with complexity and uncertainty around decisions big and small. Over time this can have major long lasting impact determining the trajectory of the business.

The equations above formed by decision theory also helps us understand the reason corporations devote major financial resources towards decision support systems. The upfront investments in IT systems and engineers might be dwarfed by the long term higher expected utility gained as a result of having access to data and information. It also makes it clear how data professionals can make valuable work. We can begin to look for those exact circumstances where it's possible to increase utility drastically as a result of improved access to information. Later in this book we will see later how businesses can operationalize this, which requires different components. 





## Summary

To reiterate we have that the core mechanism by which data creates value. It is the ability to shrink the deficit there often is between the utility we achieve with the current information and the utility we would achieve with perfect information. Equation 1.6 formalizes this deficit as the **Expected Value of Information $(E(I)$)**:
$$E(I)=E\left[\max _{a}u(a,\theta )\right]-\max _{a}E\left[u(a,\theta )\right]$$
This equation neatly isolates the economic premium of data. The left side represents our expected payoff if we could see the future state $(\theta$) _before_ choosing our action $(a$). The right side represents the best choice we can make right now, trapped in our current state of ignorance. The difference between the two is the exact upper bound of what data is worth.
