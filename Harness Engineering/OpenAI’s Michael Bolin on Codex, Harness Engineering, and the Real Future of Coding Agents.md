---
title: "OpenAI’s Michael Bolin on Codex, Harness Engineering, and the Real Future of Coding Agents"
source: "https://www.youtube.com/watch?v=6BAqgT3qe98"
author:
  - "[[Ksenia | Turing Post]]"
published: 2026-03-14
created: 2026-06-02
description: "Regarding the question of what matters most – the model or the harness – Michael Bolin is somewhere in the middle.Stronger models clearly pushed Codex to new heights. But without the right harness a"
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=6BAqgT3qe98)

Regarding the question of what matters most – the model or the harness – Michael Bolin is somewhere in the middle.  
  
Stronger models clearly pushed Codex to new heights. But without the right harness around them, those models would not be able to operate reliably, and – most importantly – safely on a real developer’s machine. At least, not yet.  
  
In this episode of Inference, I talk with Michael Bolin – lead for open source Codex at OpenAI – about the engineering layer that makes coding agents actually function: the agent loop, sandboxing, tool orchestration, and the design decisions that determine how much freedom an agent should have.  
  
In this conversation, we get into:  
What a harness actually is and why every coding agent needs one  
Can a model be enough for a reliable coding workflow  
Why do they build harness as small and tight as possible  
How Codex handles sandboxing and security across OS  
Why safety and security are not the same thing in agentic systems  
How coding agents are changing the daily workflow of developers  
Why documentation, tests, repo structure, and agents.md suddenly matter more  
Whether too much context can make an agent worse  
Why Michael believes the future may involve fewer tools, but more powerful ones  
If you’re trying to understand where coding agents are actually going, this episode is for you.  
Subscribe to the channel to be notified about Part 2, where we discuss what becomes of the software engineer in the age of agents.  
  
Chapters:  
0:00 The New Inner Loop of AI Coding Agents  
0:17 Introduction: Michael Bolin and Open Source Codex  
1:17 What the “Harness” Is in AI Coding Agents  
2:13 Security and Sandboxing for AI Agents  
4:33 Codex Launch and Rapid Growth  
5:25 The Codex App: A New Interface for Developers  
6:36 How Coding Agents Change Developer Workflows  
10:04 Writing Codebases and Documentation for AI Agents  
12:44 Context Engineering and Prompting for Codex  
16:02 Model vs Harness: What Really Matters for Agents  
19:23 Multi-Agent Systems, Tools, and the Future of AI Development  
  
\*Follow on\*: https://www.turingpost.com/  
  
\*Did you like the episode? You know the drill:\*  
📌 Subscribe here and here (https://www.turingpost.com/subscribe) for more conversations with the builders shaping real-world AI.  
💬 Leave a comment  
👍 Like it  
🫶 Thank you for watching and sharing!  
  
\*Guest:\*  
Michael Bolin, tech lead on Codex, OpenAI  
https://www.linkedin.com/in/michael-bolin-7632712/  
https://x.com/bolinfest  
https://github.com/openai/codex  
  
📰 Transcript: https://www.turingpost.com/p/bolincodex  
  
\*Turing Post\* – AI stories from labs the Valley doesn't cover.  
https://x.com/TheTuringPost  
https://www.linkedin.com/in/ksenia-se  
  
Tags: #AI #OpenAI #Codex #CodingAgents #DeveloperTools #AgenticAI #SoftwareEngineering #HarnessEngineering #Harness

## Transcript

### The New Inner Loop of AI Coding Agents

**0:00** · you know, the model is going to dominate. The harness lets the agent shine, but this is like a new inner loop that I think we're all kind of figuring out how to optimize. The agent should really be deciding what to do.

**0:11** · \[music\] Hello everyone. I'm happy to have Michael Bowlin today for the interview and he's the lead for open source codex. Michael, thank you for joining me.

### Introduction: Michael Bolin and Open Source Codex

**0:27** · Thank you. It's great to be here.

**0:28** · So, um, you know, currently people often think the story of AI coding is just the model writes code, but a lot of teams building agents say that the real shift is to designing the environment around the models. What side are you on?

**0:43** · Certainly, you know, the model is going to dominate the experience for sure.

**0:48** · There's still a lot of room for innovation in the harness, right? So, that's a pure research problem. I would say in particular for our team, it's been that relationship between, you know, the engineering side and the research side and co-developing the agent, right? Making sure that anyone can have ideas about how the agent should work, making sure that the harness lets the agent shine and do the best things that it can do and then giving the right tooling to the agent, making sure that it gets used in training so that things are in in distribution, you know, when we ship it as a as a product to the world.

### What the “Harness” Is in AI Coding Agents

**1:17** · Let's maybe define harness and why it becomes so important.

**1:21** · Sure.

**1:21** · So, yeah, the the harness is, you know, what we call the agent loop sometimes, is the bit that, you know, calls out to the model, samples the model, says, gives it the context of, you know, here's what I'm trying to do, here are the tools that are available to me, tell me what to do next. And then it gets that response, you know, from from the model. Often that's a tool call and that says, here's the, you know, the tool I want you to call with these arguments, you know, let me know what came back.

**1:44** · And, you know, sometimes these tools could be pretty straightforward, like run this executable, tell me what standard out was, what was the exit code, and that's the end of it. You know, we've done a a more experiments there with more sophisticated tools for controlling the the machine. So, they're actually controlling the user's laptop, so it's a more interactive terminal session and not just kind of simple shelling out of commands. Or it could say, you know, do this web search or these various things.

**2:09** · The harness a lot of what we do on Codex in particular because it is, you know, primarily a coding agent and we care tremendously about security and sandboxing. And so, what that means is that it's the harness that takes these shell commands or or, you know, computer use commands from the from the model and ensures that they run in a sandbox or under whatever policy the user decides to give the the agent.

### Security and Sandboxing for AI Agents

**2:35** · And there turns out to be a lot of complexity in that area. It's important that I mean, critical I'd say that we not only can, you know, expose all the intelligence of the model, but do it safely on the user's machine.

**2:48** · How do you do it when you're open-sourcing Codex?

**2:51** · Oh, the safety side of it, you mean?

**2:53** · Yeah.

**2:53** · Yeah, sure. The nice thing is you can actually see all of this because it's in in our repo. And so, we do different things for each operating system, something specific to each one. So, on macOS, there's a technology called Seatbelt. On Linux, we use a collection of libraries, something called there's something called Bubble Wrap and seccomp and Landlock. And Windows, we've actually built our own sandbox. Some of these things like Seatbelt are part of macOS, so that's, you know, not in the open-source repo, just how we call it. But other things like our Windows sandbox, the code for that is in the open-source repo.

**3:23** · And so, we, you know, orchestrate all these calls to go through the sandbox in the appropriate way for the different tool calls.

**3:33** · So, when people fork Codex, it's all baked in, all the safety rules, right?

**3:38** · Right, yes. So, yeah, I guess I should I should clarify, you know, a a detail there is there's safety and security and people use these terms interchangeably in AI a lot and they are subtly different. So, I guess the piece that I'm talking about is more strictly speaking, I guess on the security side where where you're saying, yes, you can run this tool, but you can only read these folders or write these folders and that sort of thing. I think most people in the industry would clarify that safety is actually happening more on the on the back-end side, making sure that the tool calls that the model suggests in the first place are safe to to run, right?

**4:09** · And from the hardest of perspective, it's following orders in a certain sense, right? It's it's it's a faithfully executing the tool calls, but those decisions about what tool calls are safe to run or appropriate to run are made on the model. So, yes, if you fork Codex and you're still talking to our models, then you're, you know, relying on our safety of our models, then then yes, you get that if you ran someone else's model, then you know, you're it's a little bit, I guess, a little more up in the air.

### Codex Launch and Rapid Growth

**4:33** · Got it. Since you launched Codex, how does it perform? What do you see? It's a little bit complicated. There is CLI, there is app, there is this, there is that, but in general, how the audience like it?

**4:43** · We've had a very very positive response.

**4:46** · I think it's, I don't know, like 5x in usage in terms of the start of the year.

**4:50** · You know, I mean, going back, we launched in April of last year, but it was really in August when GPT-5 came out, we did a refresh of the CLI, that's when it really started really started moving. I mean, we, you know, we had growth, but it really started jumping up. Then we did the VS Code extension later that summer fall, and that, you know, then people really gravitated towards that or that Yeah, I think believe VS Code overtook CLI usage, and then we launched the app, you know, at the start of this year, and that has really taken off.

**5:19** · You know, I think it's really the first of its kind in a lot of ways, and that's really resonating with with people.

### The Codex App: A New Interface for Developers

**5:27** · What's so new about it?

**5:28** · Developers had spent so much time in their IDE historically, and it doesn't make a lot of sense, I think, to, you know, to meet users where they are. You know, some users are in the terminal, so that's why we have the CLI. A lot of users are in an IDE, so that's why we're in, you know, VS Code, actually now integrated into JetBrains and and Xcode.

**5:44** · You know, it's kind of a a obvious and a natural place to go to to meet developers. I think with the Codex app, right, we've actually established a new surface. I like to think of it as as a mission control type of interface where, you know, now I'm managing many conversations in parallel, but I do have, you know, some key pieces of what you normally expect in a traditional IDE. So, you can browse the diff that the agent has made.

**6:08** · You can actually hop open pop open the terminal with command J, so you don't have to, you know, switch away to a different if you kind of want to do some sort of ad hoc things. You know, it's really breaking expectations that like, "Oh, I don't I don't actually have to have all my code." I mean, it's nice, but I can actually get a lot of done and there's actually more value for a lot of people in being able to, you know, to organize and and work across multiple agents. And like that's actually the thing that there is like the top priority and that we, you know, really bring front and center to people.

### How Coding Agents Change Developer Workflows

**6:36** · Well, let's talk a little bit about how coding agents and and systems like Codex change the way developers work. So, when coding agents enter the workflow, what changes first in the daily work of engineers like you?

**6:51** · Sure.

**6:51** · I mean, one of the biggest I think is throughput. I mean, just that people are really trying to They know that if you really put attention on it, right, you can you can actually get a lot of work done in parallel and kind of that incurs some amount of context switching that maybe not everyone but everyone loves, but if you can master that, right, you can really push a lot of things forward.

**7:11** · That's one is that, you know, I personally have, I think, five clones of the Codex repo that I can kind of hop between. And you know, sometimes it's a small thing that I would just saw somewhere while I was doing something else and I was like, "I really I just like to get that fixed." Or sometimes there's, you know, kind of like full day conversations where I'm kind of maybe doing a very large change and like working with Codex throughout the course of the day or kind of, you know, between meetings and you You know, a lot of people I think who does few minutes, five minutes between meetings, you might want to like, you know, send another message just to to to push it off in

**7:40** · another direction so that it that it keeps moving forward you know on whichever task that you're doing. Yeah, one is working across multiple work streams at the same time. I think another that a lot of people are spending more time on right now is then even figuring out well how do I optimize this workflow? This is this is all very new right to everybody mean relatively speaking. So investing in oh you know should I turn this into a this thing that I feel like I keep doing should I turn this into a skill or that sort of thing? Should I actually share this skill with my teammates cuz I think we should actually all be doing this sort of thing.

**8:10** · You know what everyone I think all you know good developers are always trying to find good tools and to optimize their inner loop but this is like a new inner loop that I think we're all kind of figuring out how to optimize and I am you know spending time on that but in a way that didn't exist before.

**8:24** · And then the other one that I think is very natural is how much time we all spend on on code review or the volume of code review that's one you know obviously that gets a lot of attention right now and you know for sure Codex is also doing a lot of the code review which is great which saves us a lot of time. You know figuring out how to how to make the most of that too is always I feel like a bit of a moving target right now.

**8:44** · When you was working on Codex initially were there any like interesting stories or unexpected things that you encounter?

**8:53** · You know so much has changed so Codex is still not even quite a year old right which is pretty remarkable the amount of change in that in that time period.

**9:02** · Mind blowing yeah.

**9:03** · Yeah

**9:03** · I mean you know trying to think back the models is are very big part of the acceleration that we've had. So when we launched in April of 2025 that was part of the 03 and 04 mini launch so we were using reasonable reasoning models the tool calling and instruction following like wasn't you know quite I think where we we wanted it to be and you know seeing that change over time that has been a big one. Trying to think that you asked specifically about like kind of early on a lot of those things.

**9:32** · I mean I think getting Codex to write more of Codex you know it was just such a that seeing that bootstrapping happen. You know, things like agents MD uh becoming more standard and things like that that just getting that scaffolding in place so that you're building the tool that's optimizing your own workflow that gives you kind of that exponential lift-off was just exciting and and very fun and to have certainly like colleagues like really starting to to get it and you know, shift more of their work to Codex and being excited about doing that.

**10:02** · How does repository and all the documents, how do they need to look like when an agent is navigating this instead of a human developer? Like you mentioned agents MD.

### Writing Codebases and Documentation for AI Agents

**10:11** · Yeah. What is the biggest difference here?

**10:13** · It's funny. I think an interesting thing about this whole agentic coding journey is that there are a number of practices that have been considered best practice, you know, in software for a long time and we just didn't do them. So, you know, for example, documentation is one, test-driven development is one. You know, people I mean it's not that people never did these things, right? But they they're like, well, you know, is the trade-off there? Is it worth it, right?

**10:36** · And now, you know, in an agent-first world, these things are clearly worth it, right? And now people are I feel like, you know, almost rediscovering these things that we've known about for a long time but but really caring about them. When you think about agents MD, for example, you know, all the stuff that's in there, at least that we write in ours, I would say is is suitable for a human, you know, you know, a person joining the team and things that they need to know and it's all these best practices. You know, it's nice. It's actually kind of freeing that we have to make sure we actually write these things down in a way, you know, for the agent and for our teammates. But at least on Codex, you know, you can see it, right?

**11:08** · It's kind of nice that you can just look in the repo and see what we do. You know, our agents MD file is pretty modest, I would say. On Codex, you know, we consider ourselves AGI built, meaning that we should the agent should really be deciding what to do rather than us feeding it, you know, more instruction than it needs. And so, rather than, you know, trying to write up a document that's in parallel to the source code, you know, that's potentially duplicative and and it's also potentially incorrect, right, inconsistent. The agent most of the time is a spends a lot of time re-gripping, like reading code, right?

**11:37** · And kind of forming its own opinion. So, I think we try to put things in an agent's MD that maybe it wouldn't have gotten, you know, very obviously or very quickly from the code. You know, like, "Hey, this is the way you should run the tests." Or these tests are more important than those tests, things like that. But, I think we actually try not to overdo it. Let the agent, you know, decide the best way forward.

**11:55** · So, you think in the near future agents MD will be written by an agent?

**11:59** · I mean, a lot of people's are right now, you know, or I know a lot of folks who we don't happen to do it on our our team as a general practice, I would say. You can actually, I mean, look through the the history and double-check me on that one. Many people or anecdotally hold like that they in their personal instructions say, "Oh, and when you're done, like please update anything of interest to the agent's MD file that you, you know, was not obvious or however you whatever you and your your agent your Codex want to do.

**12:27** · Feel like they're in the industry, I mean, I just see different papers coming out on People are experimenting with, I guess, even how much to tell the agent. And I'm sure it depends on the agent as well. So, but like I said, I think we take like a modest approach. It's not like tens of pages of instructions or anything like that. I think it's more like a handful of off the top of my head.

### Context Engineering and Prompting for Codex

**12:44** · What about context engineering being an important part of this process? Is there is such a thing as too much context for an agent?

**12:52** · I'm not a research researcher would give you a more precise answer, but I would give you from my from my empirical experience is that, you know, a lot of times, you know, like let's say when I'm prompting Codex, like for a like a more meatier task, you know, I probably write about a paragraph or so. And I ask it to go often ask it to familiarize itself with that part of the code. You know, maybe I give it explicit pointers to files if I think it's going to help. But but a lot of times I I don't, you know, does a good job of searching the code base. I mean, I think, you know, you asked about things you do.

**13:21** · I mean, I guess subtly trying to make sure files and folders are well named and things like that. I think I mean, again, one of those things that's just a good practice anyway, but it's probably even more important than we realize, you know, when the agent's searching the code. Most of the contents is context, sorry.

**13:37** · You know, it's going to be agents.md, my, you know, the thing that I prompted it, maybe some file references that I gave it. I mean, I do also give it access to reading GitHub. So, things like, "Hey, a similar thing happened in this pull request." Or, "I think this request regression this pull request." And so, it could also see, not just the code, but any if the conversation that happened on that pull request. But again, it's more about, I think, like, letting Codex know that has these options, here are the tools in your toolbox, but not being prescriptive about the best way for it to solve the problem, and trying to let it do its job.

**14:08** · And it's it's a good model, so you know, it does a good job there.

**14:13** · It sounds almost like it pushes you kind of toward stricter architecture.

**14:18** · Certainly, you know, Codex is going to follow patterns that it that it sees in the in the code base. You know, so if you have a good architecture in the first place, then it's going to follow it and maintain it, and force the invariants that you set up, you're going to be in a good position over time. But again, right, that's also true of human developers as well. It's just I guess it's just that, you know, the rate of change is now just so much higher, so that if you, yes, have these, you know, standards, you know, you're going to get the benefits of them.

**14:44** · Do you still see a lot of slop coming out from the model, from the coding agents? And like, how do you fight it?

**14:51** · I mean, with Codex, not trying to think of anything comes to mind. I don't think I've seen things that I would call slop. Sometimes it's just I think all these models like to write code.

**15:01** · And so, sometimes the answer is deleting code, and sometimes it's, you know, you know, maybe need to be a little more prescriptive in that way. But, you know, that's not exactly slop, or maybe it's like, "Ah, you know, you you added 500 lines to this file, maybe you should have made a new file." Like, that's those are easier fixes. But, in you know, in many cases, what's far more common is that it maybe knows an idiom or a language feature, you know, that I just happen to have not have encountered yet and it adds it and I you know, like learn something new. That is more often the way that I'm surprised by Codex rather than than stop.

**15:30** · What What you're describing is that uh since the Codex was started, the model was not there yet. Now it's much stronger model. Now it's the application itself that brings more audience. I'm trying to understand this you know, like big model or big harness. What is more important and is there a way when the harness stops being a wrapper and it just starts becoming an environment that matters more or it's still the model rules it all?

**15:56** · You know, it's possible. I mean, in a lot of ways we try to make the harness as small and as tight as possible. So, one thing that you you see in in Codex compared to I think some of the others is that we try to give it very few tools. So, for example, Codex doesn't have a an explicit tool for like reading files, right? We instead we give it control of a computer terminal and if it uses cat or said or whatever command line tool that's present on the system to read a file, we encourage it to do that.

### Model vs Harness: What Really Matters for Agents

**16:23** · I made a comment earlier about about being AGI pilled and we meaning that we give it a a large space to play in and it should find the best point in that space to move forward. In a certain sense, the harness gets smaller in a number of way or we we try to keep it small and just give it like a handful of very very powerful tools.

**16:41** · The only way perhaps we compromise on that at all is again is the is the security aspect of things is that you know, security and the sandboxing like as specifically how we approach it is a very important backstop, I would say, to just letting Codex run run wild, so to speak. Yeah, you know, sometimes people play tricks trying to do special tools to try to maybe manage the context window better.

**17:07** · Like you you feel like as the harness author, it's like, well, I know better than Codex. Like I'm going to give it I'm going to try to bias it to do these certain things, say to manage context window better. But I I would say we try to shy away from that. If say it's going to run a tool that's going to spit out a gigabyte of data, and we don't want to put that gigabyte of data into the context window cuz it's not probably relevant. I think our view would be, hey, let's let's bias Codex so that it writes that to a file, and then maybe it grabs the file or it does something else, right? And like but it's again free to kind of choose its way to solve that problem.

**17:39** · Do you think it's possible to encode all these rules in safety and building sandboxing, or there's always should be human in the loop, the human judgment?

**17:49** · For coding, for these these the the task that, you know, I you know, focus on, sandboxing is really the main thing.

**17:56** · Like is is the replacement for human in in the loop for a lot of the stuff, at least for the you know, for the sorts of tasks that we work on. You know, you have a prompt, you have a you have a problem, you have a coding problem that you give to Codex. You have this environment that it can operate in that's can you know, constrained in certain ways by a sandbox. Letting it explore that space is I think going to get you, you know, the best solution.

**18:18** · Certainly at scale, right? If you like I mentioned that you know, I have like five clones of of Codex going, if I were having to interject every few minutes on all five of those things, and you know, like then that really limits fundamentally like the throughput that you can get out of them. In training the model, I mean it is as opposed to having a human in the loop, right? We we want the models to get smarter and to do those types of things, have those corrections happening at training time that that, you know, then play out at inference time.

**18:45** · So, it will be more in the model, not in the harness.

**18:48** · So, yes. There's other parts that are important also, right? Things like the reliability of the harness is you know, a pretty big one, right? If the harness falls over, then your session's over, and then, you know, what can the model do? That sort of thing. And so, to that end, you know, performance and reliability are really important principles that we have when implementing the harness. For example, I don't know, if we want to stand up a farm of Raspberry Pis. I don't know, right?

**19:14** · Where each one's running running the agent loop ensuring that again, we're like judicious with the resources on the machine, right? So that most of the energy is spent what the model needs to do and like the harnesses ideally doing kind of like the the bare minimum there. We I think inevitably move out towards multi-agent and sub-agent and more agents talking across machines and things like that. Having the harness then is not just like a you know a single machine you know processor right now we're talking like about a network of agents and things like that.

### Multi-Agent Systems, Tools, and the Future of AI Development

**19:46** · I expect there'll be you know more interesting work to do there still. I won't be out of a job quite yet. That will change and you know and you know I personally have spent most of my career writing tools for developers, right? Now probably writing more tools for agents. The agent can obviously can write its own tools as well, but we'd rather have a small number of tools that are very powerful that it can use to explore the space well, but I think that we'll also still continue to be experimenting like what is that right you know set of primitives that we want to focus on.

**20:16** · Do you know this set already? Have you thought about it?

**20:19** · I mean I think we see a lot of the pieces there right now. So I mentioned I used the term shell tool earlier. I use it more generally as a terminal tool. So the models interface you know into like a using a computer terminal more like a human would not just straight up just executing individual commands. So like dealing with things with streaming output and and using that efficiently. The use of memory I think is I guess another you know big area that we see a lot of interesting work happening in.

**20:47** · So historically again every time you would you you would start a conversation, right? It's kind of from nothing and that's why you have agents MD and some of this context stuffing to try to get that you know information into the model very quickly. So if you look you know in the repo you can see there's a lot of experiments around memory. There's a lot going on with with different types of context connectors, right? It's like, okay, well, I originally was kind of focusing on computer tasks on your machine, but now it's also about getting work done, which maybe is, you know, sending email on behalf of your or creating documents and things like that.

**21:20** · That set of tools or taking action, you know, in a web browser. There's a lot there as well. And then things like just kind of, I think, standard LLM stuff where generally speaking more context window is good. How we compact that, you know, when you hit the limits of the context window, you know, all that stuff is still actively being pursued and contributes to the overall model, you know, agent experience.

**21:46** · \[music\]