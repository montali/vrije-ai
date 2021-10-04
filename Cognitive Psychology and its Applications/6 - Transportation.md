# Transportation
First, you may wonder why **transportation is so important** to cognitive psychology. It is a nice example of interaction between human and an artificial _assistant_. Millions of people travel every day and experience this. While traveling we often have to deal with tracking and manual control at speeds: our brain is not made to do that, so we can study how to improve the behavior in this.
The environment changes very rapidly, so we have to learn how to predict the changes and act upon them. Of course, one of the main concerns is **safety**: people travel and need safety, and the system designer has to think about that. There are other things that are interesting to estimate, as the costs of life (primary goal is avoiding life loss), and the material costs (material damages when transportation goes wrong).

## Driving
Why do we focus on driving? Driving safety is of **world's importance**: according to WHO, about 1.25 million people died from road traffic injuries in 2013. These are the ninth leading cause of death globally, and the leading cause in ages between 15 and 29.
We should try to prevent these deaths!
Looking at data, we might try to get why things are going wrong. If we focus on *high income countries* , over the last 10 years, the <span style="color:#1D7A13">***number of vehicles***</span> has increased, but the <span style="color:#D77800">***number of deaths***</span> slightly decreased. The wealth is growing and people are buying more cars, while the number of deaths suggests that the **safety** of cars increased during the years (decreasing the number of deaths!). 
If you look at the *low income countries*, the situation is different: the <span style="color:#C1FF89">***number of vehicles***</span> is increasing, but the <span style="color:#FFCB81">***number of deaths***</span> is increasing too! This means that the cars that people buy in low income structures are not as safe, and the infrastructures are worse too. 

Moreover the road traffic deaths between 2000-2013 decreases in Europe, but in other regions of the world they stay the same or not decrease so much.

### Netherlands
If you take a look at the number of deaths in traffic in the Netherlands, there was a peak around the 1970s and then a steep decrease: that's when people started to realize safety was important, with laws like the mandatory seatbelt law.
You can see that cars are producing the most deaths in traffic, but also bikes.
If we take a look at hospitalized people, bikes and cars have higher rates. Cars have a decreasing rate, while bikes don't.
It is also interesting to take a look at ages in relation to accident deaths, two groups immediately capture our attention: one is the 18-24 age group, the other is the 65+. 
It turns out that more than 90% of accidents are due to **human error**. So ad human factors engineers we can do a lot to reduce accidents in traffic. 

## What can we do?
So, what can we **improve in road traffic safety?**
Let's first do the task analysis of driving, identifying the critical issues that can be improved. Then, we can analyze these issues and the countermeasures to present them.
### Task analysis
Globally looking, driving performance can be assessed in 3 parts: **strategic, tactical** and **control**.
The **strategic** part is composed of two components: the **choice of route** (plan the route that you want to take) and the **travel time**. Strategy happens before driving, while the **tactical** aspect happens during driving. The first aspect of this is the **choice of speed** (looking speed limit, traffic around you, etc), then the **lane choice** (overtaking included) and the **turns taking** (eg. getting off the highway and going to a station to take gas).
The **control** part is probably the most important: it involves the **distance** from the car in front of you. The general rule is maintaining 2 seconds of distance from the car in front of us. Another form of control is **lateral control**, i.e. the position on the road.
Now that we have performed task analysis, let's try to understand the primary and secondary tasks. The primary task of driving is **lane keeping and hazard monitoring** (i.e. safely driving). The secondary tasks are anything else: navigation, scanning for signs, radio listening, talking to passengers...

![image-20210928181325251](res\gibson&crooks.png)

A diagram created by Gibson&Crooks was developed in 1938 illustrates the tasks. The top part is **tracking road hazard monitoring and forward vision** (Primary Visual Attention Lobe). This is related to your attention, as the primary task is this. As mentioned, you have two ways of controlling your vehicle: longitudinal and lateral. 
Everything else (bottom of the graph) are non-visual tasks, such as auditory, cognitive and motor tasks, which are competing with the primary task. Another important concept seen here is **TLC**, the time to lane crossing, and the **Time to Contact**, i.e. how much time it will take to collide with the vehicle in front of you. 

## What we can improve
We now know that the primary information stream is the **primary visual attention model**.
The **visibility** is the first thing to improve, and we can do that in 4 ways: anthropometry, illumination, signage and resource competition.

1. *Anthropometry* is the first one. When the first car was designed, the aim was having a *one size fits all* product. This is not always possible: the person has to be able to see well, both the world and the dashboard. The design of the **interfaces** is crucial: the dashboard, the chair, the wheel... A lot of work is going on to design the perfect interface. 
2. The second thing that can be improved is *illumination*: driving at night is 10x more dangerous, so proper illumination is very important. Some estimates suggest that outside illumination can decrease accidents two-fold.
3. Another important improvement is *signage*: this has to do with road signs, aiming at easy extraction of information from them. We have criteria for the design of these: 
   - the first one is **readability**, having to do with limitations in perception/attention. 
   - Another problem is **clutter**: the signs have to stand out, as the proper sign should be easily findable by anyone. You can remember the distinction between feature search and conjunction search: if there's a lot of signs, we get confused. 
   - Another important factor is **redundancy**: for example, traffic light both have color information and spacial information. Redundancy is used to facilitate information processing, as you can only process one part of the stimulus and still be okay. 
   - Another important aspect is **consistency**: unfortunately, not everybody has the same traffic lights! If you were coming to a different country, you would be confused.

Visibility is very important, but how do we **measure it**? One of the measures is **eye tracking**. One study has researched how long it takes to carry out different visual tasks while driving, and you can see that the glance duration varies among the tasks. The general suggestion is that the glance should be shorter than 0.8s, and there should be more than 3s between glances. The risk of have an accident is roughly proportional to ${time_{glace}}^{1.5}$. 

![image-20211003180625617](res\measure_visibility.png)

The main task is always safely driving. This provides an interesting way to have some estimates of distraction. 
One last thing to talk about is **resource competition**: this is important, and it has to do with our attention's limitations. All the different things in the car are competing with our attention to the road, for example head-up displays (speed and temperature projected on the windshield), hands-free cellphones, audio warnings, speech controls...
The biggest danger to our attention nowadays is **using smartphones**. How can we measure this response competition? So how can we convince people not to use their phones?
Using a driving simulator, we can do research on this. In a study from 2001, participants were driving in a simulator, and they had to hit the brake when they saw the car in front of them braking. Experimenters measured the reaction time, comparing single task condition vs dual task condution: 

- *single task* means driving and break when see red lights
- the *dual task* concern having a conversation on the phone (using a hands-free system) or listening the radio while driving

![image-20211004125418251](res\experiment_driving.png)

The results showed a significant difference in the tasks, and we can see that in the cell phone conditions there are many more errors than in the radio control condition, and there are less error for the single task condiction. For the reaction times, the pattern is similar: participants took longer to detect the braking light in the cellphone condition!
While this is already quite convincing, the researchers also had a follow-up looking at more direct ways to identify limitations in attentional resource: to do that they measured brain activity using EEG, and the ERP (Event Related Potential), components related to external/internal events.
To plot these ERP, you need to extract the time snippet belonging to the event of interest, and average all the events. Doing that, several ERP components emerge: the one component of interest is P3 (happen around 300ms after stimulus). This has been studied extensively, and it's reflecting the amount of resources that are available for information processing. The interesting step was measuring how the resources measured by P3 are reduced by cell phone usage. This was conducted in a driving simulator with an EEG cap. ERP was time-locked to the onset of the braking light. The results showed that there's a huge difference from single task (driving only) to dual task (driving while using the cellphone).  When you are using the phone during driving, the same stimulus of see brake light induce a much smaller P3 signal.
This suggests that people are _unintentionally blind_ while using a phone. 

![image-20211004130600977](res\inattentional_blindness.png)

## Hazards
Now, we can talk about how to improve our **hazard detection**. 

One hazard is **overcorrection**: when you are getting off the road, and try to get back on track, it may happen that you overcorrect your steering. This can just be avoided with proper training. 

The other two common hazards are **fatigue** and **speeding**. What is common among these 3 hazards is that they all lead to loss of control. Most casualties occur in these situations. A lot of care should be taken into avoiding loss of control.

### Fatigue
This is a very common cause, having to do with loss of vigilance. It mostly happens during the night: the driver should be well rested when driving. That's why it is important to be in good shape when behind the wheel. What can one use to counter react to fatigue? 

The first rule is obviously not driving when tired, but there are others *countermeasures* that you can take:

- One are the **rumble strips**, the strips on the side of the road that wake you up when you go over them with your tires producing a noise. 
- Another countermeasure is **driver state monitoring**: this is more and more common in modern vehicles, in which a camera monitors the driver's fatigue. For example, the blink rate, the size of the pupil, the closing of eyes...
  The car can then provide an alarm to the driver. 

**Speeding** is another common hazard: it is of course dangerous, as it can lead to loss of control. Another danger is that you're traveling so fast that you cannot anticipate hazards and don't have enough time to react, as you travel further in your reaction time. Of course, you also create greater damage at impact. 

Why do people actually speed? There are reasons, groupable into **perceptual** and **cognitive**. The perceptual reason is that you may not perceive the speed: for example, when you get out of a highway you tend to go faster in the city.  There can also be cognitive causes, for example **not knowing the speed limit**. Often, we have to talk about **risky behavior**: people engage in speeding because they underestimate its danger, and they're overestimating their driving skills. Younger drivers have tendency to speed, as they're underestimating the danger, and they don't have much experience. They also do not have an adequate mental model for hazards, so they do not know what to expect. 

What are **countermeasures** for this? Beside the fact that if you go over the speed limit you can get a fine, you can use **cruise control** and **safe distance**. The rule is that the safe distance should be 2 seconds to collision. You may wonder why 2 seconds: the reaction time for braking is usually around 1.5s. We add 500ms, a _positive safety margin_, representing the time that we add to account for unpredictability in the real world. 

## Individual factors
Up until now we've talked about visibility, hazards, and so on. 

We can now talk about **alcohol use**: in the US, it's cause for 50% of fatal accidents. Just the legal limit of 0.05% leads to poor reaction times, tracking and information processing. There are different ways of dealing with these, like speed limits, fines and social pressure. The most important factor that has worked is the latter: if it's considered to be **not cool**, and you peers do not drive under the influence of alcohol and correct each other, things work better.  But this still remains a big problem. 

Other factors are **age** and **gender**. It's been proved that driver fatalities plot as a function of age and gender. You can see that most fatalities occur for younger adults, and the difference between genders starts to be perceivable around 20 years olds and disappears around 50. For both genders, fatality goes up after 70. So, what are the possible reasons for this? We can split the causes according to the drivers age:

- *Young male* drivers are especially risky: they have inexperience, overconfidence and risk taking. They tend to underestimate their abilities, resulting in more probability to drive with alcohol in the blood, fatigue and driving at night. They are also more prone to distraction. 
  This is very problematic and has to be addressed with proper campaigns. 
- *Older drivers* are also at risk, for different reasons: they have vision problems, terrible reaction time and worsened attention. They are usually more experienced, though. Attention is the biggest problem: one famous study proved that the _Useful Field Of View_ (i.e. a concept relating images to attentional processing, having nothing to do with visual abilities) is reduced for older people. This means that older people tend to concentrate on the center of their visual field, resulting in less information processed. Younger people were able to detect targets in the center and periphery both. Older people had narrower field of view: the performance was normal in the center, worsened in the periphery. Age decreased this field of view dramatically. This UFOV was used in DMVs too (the organization in USA that administers vehicle registration and driver licensing). 

To summarize, the **safety improvements** can be presented in the following table.

They can be implemented in different sides (driver, vehicle, road) and times (predictive, during the crash, post-crash).

![image-20211004150322026](res\safety_improvements.png)

## Intelligent systems
There are several types of **intelligent systems** that make driving safer: the cars are starting to have systems like _lane departure warnings_, _lane centering_, _collision avoidance_. The cars are also equipped with _navigation systems_, which reduce the effort of the driver (even though it's a distraction, since driver need to monitor it), having up-to-date information about traffic, weather, services...
There are even self-driving systems available, which in the next years will heavily improve security.

## Summary
We talked about transportation and driving, which has been presented as a human factors problem. There's still a lot to do. The human is still a big part of the interaction, so we have to think long and hard how the role of humans will change in the future. We talked about the primary and secondary tasks of driving, and how to prevent the latter to subside. We talked about the tools to analyze and improve human behavior while driving. 