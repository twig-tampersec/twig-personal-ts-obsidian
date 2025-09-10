---
author: Jonathan Happel
---

## Vision

Reduce risks of AI arms races by creating a hardware security solution that enables nation states to verify what they are doing with their AI hardware.

## Mission

We’re currently building a platform that is secure enough to withstand nation state actors (high sensitivity and high specificity) which aids AI verification.  
We are unsure about the exact application, hence we build it flexible.  
Example applications are:

* Enclosure around NVL-72 Rack  
* Enclosure around Camera  
* Enclosure around Differential-Power-Analysis Sensor

## Heuristics for technical development

If I needed to summarize it in a few key bullets:

* Security against nation-states is non-negotiable\!  
* For anything that has a critical function: a) have a roadmap to reach this critical function, b) have a scrappy placeholder or c) skip it for now. Don’t get stuck between a) and b).  
* Modularize; we want to engineer a solution once and then copy paste it for future iterations  
* Space Constraints & Integration Constraints are way more important than you think  
* Cost per Unit is way less important than you think

Full details:

* General TamperSec Engineering Priorities  
  * Low Development Cost \> Short Development Time \> Low Cost per Unit  
  * Do it in-house if it massively speeds up development time or builds critical know-how that allows us to think out of the box. Otherwise, outsource  
* When making architecture decisions:  
  * Security \> Space Constraints \> Integration Complexity \> Cost per Unit  
    * Security is non-negotiable.  
      * Our target is the following:  
        * We need to be able to deter attacks from an attacker that has 1000 people that try to break that enclosure, with 1billion USD of funding, with access to currently classified technologies and trying to break if for a couple of years  
        * We also need to anticipate that an attacker might covertly insert “noise” that triggers false positives, so that the end user gets annoyed and doesn’t use our enclosure anymore  
      * Our roadmap needs to be set up so that we aim to defend against those attacks  
        * Please escalate it asap if you think there is room of doubt whether we’re on the right track for that  
        * We don’t need to have everything included right now, but we need to feel confident that we don’t waste time on anything that will never reach that standard, and also that we don’t lock ourselves into an architecture that doesn’t support such high security requirements  
      * Keeping options in might to be able to do field-replacements if vulnerabilities get discovered seems quite useful  
    * Space Constraint is one of the repeating key critical issues. We won’t be able to sell an enclosure if it adds 10cm of thickness on each side. The general heuristic is that we’re always too thick, and you want to second-guess whether there’s an alternative approach that would enable us to make slimmer enclosures.  
      * That said, don’t hesitate to use “bulky” off-the-shelf components for now, especially if it’s modularized sufficiently so that we can later add a custom, slim solution as a drop-in replacement for the currently bulky component.  
    * Integration Complexity will kill any real-world deployment if it’s a pain in the ass  
      * One Product Manager at AWS once told me: “You are doing what?\! AI Hardware is the most in-demand component across our hardware stack. There is no room for error, and no room for major downtime\!”  
      * Data center operators are very sensitive to uptime, and if we engineer a solution that is very shitty for maintenance (or installation), then they likely don’t want to deploy it at all.  
    * Cost per Unit is last\!  
      * This is a moving target, but generally speaking, as long as we don’t use lithography-based meshes, I’m not that concerned about cost\!  
      * I.e. a NVL-72 racks costs \~$5Mio. A sales price of \~50k for such an enclosure would be very reasonable. And a sales price of \~500k would be within the overtone window. We need to subtract some margin from those numbers, but a 5-figure USD amount will bring us a very long way if we are building enclosures based out of PCBs\!  
  * Modularize\!  
    * We don’t want to engineer a certain function for each individual use case. We want to engineer it once, and then integrate it for future iteration again\!  
    * The fewer constraints there are, the easier we can upgrade any individual component  
      * This is great from a rapid-prototyping perspective\!  
        * We can right now use off-the-shelf components that don’t fit into the envisioned end product (e.g. due to space constraints), but is just way easier for us to prototype with right now. With a modular system, we can later easily replace those components once it becomes necessary  
        * We can also use a very scrappy version that only fulfils part of the requirement and later replace it with another version that properly fulfils all the requirements  
      * This is great from a development effort perspective\!  
        * If we do another iteration, then   
    * The more modular we are, the easier we can adopt parts of the system without re-designing everything  
      * E.g. I don’t want to re-design the mesh routing for every iteration just because the size of the panel changed, and I also don’t want to use different EMI shielding methods for each iteration. I’d like to engineer it once, and then copy it to future iterations.  
* When making decisions about what to include in the current iteration  
  * General Priorities  
    * Flexibility\! We want to build a platform that can serve many different applications (with different sizes, different space constraints, different  
    * Dare to reinvent the wheel, but only when necessary, and if so, build on the shoulders of giants\!  
      * Whenever possible, use existing technologies if they can fit our use case. Otherwise, development costs will skyrocket for a small marginal improvement in cost per unit.   
      * Especially use an off-the-shelf solution when there is some kind of “interface”  
      * A common argument to not use a standardized solution: Space constraints  
      * If we need to re-invent the wheel, then seek outside help from people who know how to solve the problem\!  
  * For any custom development:  
    * It either needs to have a solid pathway toward top performance, or it needs to be a modular solution so that future modules can be added or replaced without redesigning the whole system  
    * Anything that’s customized: Happy to spend on parts, but unhappy to spend engineering effort to make something customized  
      * This is a bad return of R\&D   
      * Customers are generally unhappy to pay for it  
    * We don’t want to spend engineering effort on something that we’d scrap again in a couple of months. If you for example think that our current approach will never reach a certain attenuation target but we need that target from a security perspective, then I don’t want you to spend a lot of time on a subpar approach. Either find a scrappy solution to get something demo-able but don’t spend much time on it, or don’t include it at all, or go all in and understand what needs to be done to get to the desired attenuation (and if so, likely seek outside feedback to be get it right without a lot of trial and error). Spending time to reach some subpar standard which won’t cut it in the long run is wasted time.

