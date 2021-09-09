# Human Information Processing

HIP has lots of advantages but limitations too: you can build the best system in the world, but if the HIP cannot process it, you have a useless system. 

Our brain has inputs/outputs (for example, eyes process light and informations reach the back of the brain, which propagate to other sides of the brain later), specialized areas that deal with these inputs. We also have outputs, like the frontal lobe which is sending signals to muscles. Besides these inputs and outputs, there's lots of processing, and higher cognitive functions (attention, memory, decision-making) are not usually contained in **one specific area**: generally, they are widely distributed.

Some parts of the brain are more involved than others: for example, the parietal lobe has been linked to attention. ![brain](./res/brain.png)

Generally, we'll want to talk about how sensor information is fed to **perception** (first *software layer* in our brain), i.e. systems that help us to make *interpretations out of information*. After the information is parsed, we can actually process it in detail (selective information) and eventually to decision making.

Of course, memory allows us to have continuity in our decisions. We have two types of memory, **working memory** (active state, constantly available, like a RAM) and **long-term memory** (indefinite time of storage, very large capacity). Things that we have in memory also **bias** our information processing!

 ![hip-model](./res/hip-model.png)

Our system needs **resources** too, some kind of *juice*.

We'll now have a look at the stages: first, **sensory systems** (visual processing), then **attention** (how we select information) and **memory**.

## Sensation

If we look at the light that hits our retina, we can see that only a small portion is actually **visible to us**. We are already imposed some *limitations*, therefore. To do this, we have (most people do) different areas  (cones) in our eyes that process different wavelengths. The cones also have a tuning function (they respond to a range, not a specific wavelength). Most people have **three cones**, having **Unaffected Color Vision**, but there's people having **only two cones** (color blindness). When you design a system it's useful to **run it with color filters** to see if colorblind users can see things right. Besides these limitations, we have limitations linked to **how our retina is built**: it is not homogeneous, only in the **fovea** (small portion of the retina) you're able to see **high resolution** and **color information**, as this area contains the highest number of cones. Evolutionary processes are responsible for this: it would be really **difficult to process the whole sight field**, so evolution brought us to make this distinction between the center. At the same time, we evolved a really good system that moves the eye to the relevant informations pretty fast, without having to think about it.

We have a **blind spot** in our visual field, located about 12-15º. Our brain usually fills it in as it does with colors and shapes.

## Perception

Our perception happens to trick us often. 

For example, one would like to know how do we reconstruct 3D information from 2D. There's multiple possible answers: accomodation, high convergence (to focus on the object, we move our eyes inwards or outwards) and the most famous one being **binocular disparity** (there's difference in the images seen by the two eyes, as seen in 3D glasses).

Of course there also are **pictorial cues**, often used by artists. One of them is **linear perspective** (you have two lines going away from you, they seem to get near), **relative size** (perspective gives us hints about size), **interposition** (if an object is in front of another, it's closer), **light and shading** (gives us a lot of info about 3D) and **textural gradients** (if you look at the trees they seem to get denser).

![pictorial cues](./res/pictorial cues.png)

### Gestalt laws of grouping

This is really important in software design and UI. 

- Law of **proximity**: if you organise the dots differently, the close ones seem to be grouped![proximity](./res/proximity.png)

- Law of **similarity**: here, you use contrast, and the dots that are similar in color seem to be grouped. It even works for shapes, colors...![similarity](./res/similarity.png)

- Law of **closure**: you can clearly see a circle and a rectangle, even if they're not there. We don't need to see the whole object. This is also seen in logos

  ![closure](./res/closure.png)

There's other ones: **enclosure** (if you enclose a subset into a rectangle, it becomes a group), **simmetry**, **continuity** (lines get completed in your head), **connection** and **figure&ground** (people can switch foreground and background).

![gestalt](./res/gestalt.png)

### Affordances

Another important concept. Right now we were talking about our perception being **passive**, taking sensor input and applying some kind of processing. This is not the case: we are active observers, we move around, we experience different viewpoints and **act to understand**.

We percieve something, and we want to **act upon it** to get feedback. It's also useful for design: for example, color-coded recycling trash cans don't usually work, but a certain opening (e.g. bottle shaped for glass) will. Keep in mind that people want to **interact with things**. 

### Predictions

We have been talking about **predictions**: this is probably the most important function of perception. We are so used to processing faces, that we need a small amount of information to process one. We use information from surroundings to fill missing information. We can be **primed** by having an immediate experience of seeing for example a human, if we then see a blurred face we quickly notice it. 

Up to now we've been talking about vision, but auditory information works the same. 

## Attention

When you think about it, we are aware of our surroundings and we feel like we're not missing anything. **This is not the case**. The trick is being able to tune our attention systems such that we're paying attention to the right things at the right time. The problem is that we have a limited capacity of processing information, so there's a bottleneck in our information process stream. 

People tried to define **attention** for many years, but basically we can define it as selecting which information is processed, and which is ignored. How do we actually determine that? To what extent is attention selective? A lot of research comes from *audition*, and some real life example is the **cocktail party problem**: imagine you're at a cocktail party and you're able to focus on the person you're talking to, and completely ignore the others. If somebody all of a sudden calls your name, even though you're in a conversation, you are able to hear it. *Cherry* concluded that if you get different type of information in each ear, one to ignore, the other to remember, when you ask people they cannot report them. A lot of aspects went unnoticed. His work was also used by *Broadbent* who brought vision into the research: he formalized the *Filter Theory*, stating that you have many types of perception and you're able to block some of them and only keep those you need. Is it really an early filter? Do other things slip through? Treisman played a little trick on the Cherry experiment: in one ear she started with "*In the picnic basket she had...*", and the participant reported a mix of the two sentences, starting it with the picnic basket thing though. 

Her theory still didn't ask the question *"How's this filter set?"*. Some people proposed that all the inputs are processed, and only later on (when we make choices) we apply attentional selection (*Deutsch & Deutsch*).

We like to pay attention to certain locations (it's easier for us) and put distracting informations further away. Sometimes we have to pay attention to different features, such as color, orientation, size...

This is the reason traffic lights work: you're attaching a certain action to a certain color. Human Factor Design has been applied to traffic lights: the green light is always at the bottom. 

All these different ways to select information can be quite complex: one task that we're constantly engaged in is **visual search**, for example to find an orange cup on a desk. By doing this research, we can actually figure out how the sampling works. There are two types of search, one is called **feature search** and the other is **conjunction search**. The first is easy: if you're looking for a blue circle, you'll be really quick in finding it if it's unique. There's feature maps in our brain from which we're able to extract features that we need. This is very efficient. If you have to search again for the blue circle, but it's now surrounded by distractors (blue rectangles, for example), you'll find that it's now way more difficult. You'll have to **integrate information from different feature maps**, in this case shape and color!

![feature-vs-conjunction](./res/feature-vs-conjunction.png)