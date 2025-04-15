---
title: "Reflections on WeWork: Relentless Change and Unrealized Potential"
date: "2022-08-14 17:17:00 -0400"
comments: true
categories:
  - Tech
tags:
  - Software
  - Teams
---

I spent three years as a software engineer at WeWork. Three years is north of 6,000 working hours and this post is an account of my time there and key takeaways. If you are interested in what the experience of working in a hyper growth company feels like, this account may interest you.

**Getting There**

Working for WeWork is difficult to summarize in a single sentence, or even a paragraph. A fervent energy permeated the whole company, driven by the charismatic CEO Adam Neumann. There has been a lot that has already been written about WeWork, but every viewpoint provides something new. Mine is that of a software engineer in WeWork’s tech org, shipping software during the ups and downs as WeWork attempted to blitzscale the world's fastest growing real estate business.

Having joined WeWork from Braintree, I had more experience with established companies with proven business models, operating at the scale of web commerce. The relative stability and nature of industry meant that an engineer's contributions would be making small and incremental progress with few opportunities to build something from the ground up. I was recruited by a longtime friend who was a director of engineering at WeWork. It felt like a good opportunity to experience engineering in a hyper-growth company.

I remember my onboarding day, easily the most boisterous one of my career. The host had an insatiable level of energy and it was fascinating to see people working in a whole host of disciplines, legal, architecture, design, real estate, tax all brought together in one room. At the end of the day, Miguel, one of the co-founders, came and spoke about how WeWork started. Having seen tech culture in past companies, there was already the sense that this company would be different from anything I had seen before.

**Trial By Billing**

The first team I joined was building billing in house at Wework, and it was a challenging experience for my first six months of tenure. We were working in a monolith with poorly defined domain boundaries. During its growth phase, WeWork optimized for flexibility offered to members in terms of lease agreements, discounts, and payment methods. However, the infrastructure felt the weight of this product growth, making ongoing development a challenge. The team had doubled in size in a very short time, resulting in a high proportion of engineers new to the company.
Everyone I worked with was smart and genuine, and there was great camaraderie across the team. It felt far more familial than I've ever encountered before in my career.

*Wework tech org managed to hire a group of genuinely good, talented people. This cannot be taken for granted at any company.*

My job was to tug away the billing codebase from the rest of the monolith. This was an exercise that was doomed to failure, not least due to an arbitrary deadline that was laid down on us. We toiled hard, made a valiant attempt at taming the Spaghetti monster codebase responsible for processing hundreds of millions in recurring revenue.

By January, leadership saw things differently, and decided to take the work from our humble four person team to the Tel Aviv office and dedicate an entire new department towards solving WeWork's billing conundrum. That department would eventually grow to over a hundred people, engaged in a multi year effort to architect billing at WeWork.

*Your view of the work you and your team is doing may be wildly different from how the key stakeholders see the work.* Leadership changed their priority often during WeWork, making it a constant guessing game when the product direction would change or a re-org would happen. For a company of WeWork's valuation, the rate of change was that of a small startup struggling for identity. This caused stress for those engineers who wanted to focus and specialize in a product area for a long period.

**WeLive**

As I sought out opportunities within the company, I learnt of a new effort at WeLive, the residential arm of WeWork. WeLive felt like an opportunity to build a product from the ground up, stay close to users, work with a nimble team and be a startup with large company resources. Sounds too good to be true?

It was. It was really great for a while to have zero red tape and build what users wanted. We worked on a product which had a real consumer need and potentially a massive market, but ultimately the environment was not a fit for what we were building. As WeLive failed to expand at the rate of WeWork, business drying up meant that it was no longer possible to budget a technology team and incur millions in operating expenses.

At the same time, top level leadership became completely invested in a new redesign of the WeWork app. This meant our team was rolled over into that org, into a team that would provide core services for the WeWork member app.

We would lose the autonomy and purpose which drove us during WeLive. However, we would now build infrastructure to support all teams building products for half a million WeWork members.

**Platform**

The core team, with primarily senior/staff engineers, was a very competent team. We lacked a clear mission or agenda though and became the fail safe of everything that would fall through the cracks of the product teams. Secondly, the team members began proving themselves to be too competent, so we started losing team members to higher priority product initiatives. There was a period of a couple weeks when we lost all three of our mobile engineers. In the midst of all this, we managed to launch a service to offer feature gating and experimentation in the WeWork app. We changed the way every single feature in the WeWork app got launched, and began accepting consumers beyond the app.

However, the steady loss of key members was a sign and by December 2018, it was clear that we were in the shadows where the product teams delivering the app redesign were in the limelight. A re-org would soon follow, and we would become another product team contributing to the WeWork member app.

The next step in my journey was being involved in the re-architecture of WeWork’s internal social experience used by its hundreds of thousands of members and community managers. The existing app was built in Angular 1.5, and was a maintenance headache. The groundwork would be laid for a modern app using React, while building up a component library which could be plugged in to create key experiences for members. After working primarily in backend development at WeWork, I was keen to do more frontend work, and took on the challenge to work amidst a group of capable frontend engineers.

The next few months were quite enjoyable. All of us believed in the work, and this resulted in a lot of momentum and collaboration in the team. There was a lot of emphasis on laying the right foundations, and the team was very engineering-driven. Perhaps too much so though, and design and product were not as invested in the project as engineering was. A lack of centralized focus towards delivery, coupled with changing designers meant a lot of work had to be redone. Changing priorities meant the project was resource constrained, and the full rollout of the app would get delayed by a year.

*Rewrites are expensive. Weighing in failure scenarios can help derisk this.*

**Intents**

Around this time, my manager has been discussing with me the possibility of promotion. Since I was in a new team, under a new management structure and using a new software stack, my relative contribution made the case harder to make. The advice was to seek out opportunities where I could have a higher relative impact and drive bigger results to make a stronger case.

*Your relative impact in a team matters, as one becomes more senior, staying fullstack/generalist is challenging. Specialization can be a faster path to level up.*

My opportunity came in the form of a curious word: Intents. The product leader for Member Apps had the vision of taking our member facing feed from plaintext to a variety of structured posts, evolving towards a marketplace. From one type of posts, we would go to a multitude of posts on the feed, and the grouping was called Intents. It made a lot of sense for WeWork to have, and needed experienced backend contributors to architect the level of flexibility and dynamism required.

What followed was a tragic case of misaligned expectations and poor timing. We were staffed generously, with solid talent and the rest of the org shielding the team from adjacent work streams.

Product wanted a flexible way to experiment with a large number of posts types without needing to ship a build to the app store. This key requirement meant that frontend, backend and design got involved in a month-long debate on how to execute this, since we lacked a design system and component library. We also lacked expertise in the company on how to build such a system. We eventually adapted the server driven ui paradigm. Lot of draining days fine tuning the architecture meant that we learnt a lot about division of responsibilities, managing state and the best UX for users.

However, the timeline engineering came up with was mysteriously cut short by exactly a month. So we hurried back to the drawing board, cut some key aspects to refit the project and came up with a compromise. Upon agreement, we were off to the races.

After a strenuous and heads down period, we delivered the project, two weeks over time, but something we were proud to ship and began to roll out the feature to users in September. Initial engagement of the new posts were 3-5x regular posts, which made our effort a success. However, it did not sufficiently impact the overall strategic move to increase engagement holistically in the WeWork app.

*Near term momentum for a project or team does not necessarily ensure its success and sustainability.*

**IPO & Layoffs**

In September, everything changed as WeWork went to file for an IPO. Everything else became a side show as in a period of weeks we went from a unicorn to a laughing stock on the street. The change in mood in the company was palpable and dramatic, and within days the unthinkable happened with Adam Neumann leaving the company. New leadership from Softbank came in and layoffs were in the picture. All these meant that Intents would be on their way out as the WeWork app would pivot to a utility first app.

Layoffs happened late November, right before the holidays. Surprisingly, engineering was mostly unaffected. December and January were months of struggle, barely enjoying the holidays as I worked to sharpen up for interviews.

Multiple posts can be written about interviewing and negotiations. The biggest piece of advice is to test the market regularly, use inner channels and never immediately rage quit. Long story short, by March I had my job search wrapped up and could breathe again and contemplate when to leave.

However, there was one more story still left for my journey at WeWork. After a big reorg, I had shifted over to the messaging team. Despite our failure with Intents, our engineering effort was lauded and I got promoted.

**One Last Dance**

In March, two things happened. One, in an aggressive plan to cut costs, WeWork decided to migrate all applications from Heroku to an in-house Kubernetes based hosting solution. This meant a swat team would form, responsible for shifting over a dozen apps and databases. Not one to pass up a sharp learning curve, I joined the team. My last act at WeWork would be working on devOps after being a product engineer during the entirety. Two, the Covid19 pandemic would sweep across the globe and cause everyone to shelter in place in NYC.

The next few weeks were whirlwind, as we dug into a lot of legacy infrastructure, taking stock of compute and storage resources, dockerizing apps and getting them ready for migration, all the while familiarizing ourselves with a whole host of new Kubernetes tools. After putting in long hours for a few weeks, we pulled it off and migrated all the applications by April. Despite the intensity of the effort, I learnt a lot and enjoyed work after a while. Performance and reliability is more in the realms of science than engineering, and a stark contrast to product work. I would often go to sleep still thinking about performance tuning.

My time at WeWork was great at times but overall, it was the story of unrealized promise and potential. On one hand, the diversity of problems and the great coworkers made for a dynamic and rewarding journey. However, it was frustrating to feel that in aggregate, it could have been so much more. I hope this account will help someone looking to join a rocketship, driven by leaders with Messiah complexes.

**Postscript**

**Growth**: The growth trajectory of the WeWork tech org was astronomical. During my time, it would grow 6x over two years and eventually shrink down to one third its size over the period of a few months.

*Engineers would benefit by taking stock of how their organization is growing vs what is being delivered. A sustained mismatch means a correction is due.*
*There are many incentives that can drive growth in an organization, and it's worth thinking about if you align with those incentives.*

**Extracurriculars**: This writeup has been primarily about work, but extracurriculars were a big part of the WeWork experience. Perhaps the most grandiose of those were two yearly events, Summer Camp and Summit. Both events had the entirety of WeWork employees experience product demos, mission pitches and celebrity appearances. Despite its reputation, I really enjoyed my two times at the UK version of summer camp. It felt mind boggling how a company could afford it, but it was a fun choose your own adventure weekend in the idyllic English countryside.
Startups are created in the image of the founders, or the founding team. Think whether you would align with the founding team, because that is the culture that will seep in across the company.

**#personal-finance**: My second week at WeWork, I started a slack channel to discuss personal finance. Over three years, that channel grew to over three thousand people helping each other on their personal finance goals. It was also a great case study of watching a community grow, from early adopters, to hitting critical mass, and then gathering enough momentum where it would influence company wide initiatives, such as instituting a 401k and eventually 401k matching at WeWork. It was one the most gratifying things during my time there.