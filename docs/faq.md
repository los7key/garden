---
layout: post
title: FAQ
description: FAQ
date: 2022-04-01
Last Updated: 2023-02-20
---

Really, there are questions that need to be answered. I suspect I'm going to have to put things in categories at some point or it will get out of hand quickly.  This is a work in progress.

2022-10-30: New look and broke it up to categories, we'll call this v2.0.  Don't worry, all the old questions have remained, they've just been shuffled around to where they will hopefully make sense.

***

## Life

??? question "Q03. What is the answer to life, the universe and everything?"
    42.<sup>2</sup>

??? question "Q06. How long should you wait to go into the water after you've eaten?"
    At least 30 minutes.

??? question "Q09. Why is the sky blue?"
    Sunlight reaches Earth's atmosphere and is scattered in all directions by all the gases and particles in the air. Blue light is scattered more than the other colors because it travels as shorter, smaller waves.

??? question "Q10. What is the definition of a will?"
    <div id="Q10"></div>A dead giveaway.

??? question "Q11. How much Red Bull can someone drink and not die?"
    According to [Caffiene Calculator](https://www.caffeineinformer.com/death-by-caffeine") I can drink 170 cans and still be safe.  Although, I'd probably be pretty sick.

??? question "Q16. If milk goes bad if not refrigerated, why does it not go bad inside the cow?"
    It won't go bad per se, but if a cow is not milked regularly, it can eventually stop production.


## Me

??? question "Q01. Do you really need an FAQ page?"
    <div id="Q01">No, but I love FAQs!  Also, the [introduction](/) doesn't cover everything.

??? question "Q02. Who are you?"
    I'm a security enthusiast, sysadmin, veteran, father, husband, tinkerer, and all around geek. A jack of all trades (and master of none).

??? question "Q04. Don't you have anything better to do with your time?"
    What is a better use of my time other than giving my unwanted opinion?

??? question "Q05. How often will there be a new post?"
    When the mood strikes me.

??? question "Q07. What kind of music do you like?"
    Depends on my mood and who I'm with.  Pretty much anything but country.

??? question "Q08. What's wrong with country music?"
    So many things. I've tried to like it and I've worked with people that listen to nothing but country. It's just not my thing.

??? question "Q13. Cats or dogs?"
    Cats.<sup>3</sup>

??? question "Q17. Are you an expert on cows?"
    No.

??? question "Q18. What about cats?"
    I like them, but not really an expert.

??? question "Q30. Do you know how to pick locks?"
    <div id="Q30"></div>Why yes, yes I do. At least, I know the basics<sup>7</sup> and have some of the equipment.  It's one of the [hobbies](/hobbies/) I've collected.

??? question "Q31. Why do you share all this information in public?"
    Aside from my feelings and opinions, I suspect most of my personal data has already been compromised as part of a breach somewhere.  As for the rest, I usually give opinions out for free, might as well have them all in one place.

??? question "Q33. Why does it seem so long since you've had any new content?"
    This is why there is no RSS feed or newsletter.  I write when I'm in the mood.  I don't want to force it by trying to write when I'm in the right frame of mind.  You get what you get. 

## Site

??? question "Q00. Why ~~does~~ did this FAQ require you to hit refresh again to see the answers?"

    Because I ~~don't~~ didn't know enough JavaScript to fix it. I already spent way too long on getting the look I had in mind, so I'm not ready to abandon it just yet. Don't worry, I'll get around to it in all my copious spare time™.  In the meantime, both visitors to this garden will have to refresh the page twice before the answers will be visible. This is probably the most first-world problem I can think of. If this bothers anyone you can file a ticket with our support team.<sup>1</sup>

    Update 2022-10-30:  I fixed the JavaScript problem by removing it completely haha! I just used markdown a native [Material extension](https://squidfunk.github.io/mkdocs-material/reference/admonitions/) (that I was already loading).  As usual, I was making it way too complicated.  I might change the green color later, but I kinda like how it looks.

??? question "Q19. Why is this place called "Cat Elevator"?"
    One day I was picking up my cat and the name just came to me.  Seemed like a good fit.

??? question "Q20. I skipped the [intro](/), what is a digital garden?"
    <div id="Q20"></div> For now, you'll have to rely on the intro. I might write more about it later™.

??? question "Q22. Who is the intended audience of your "garden"?"
    I am.  I was going to add more to that sentence but then realized, it's me. Then I realized, I need an [about](/about/) page.

??? question "Q23. Why do you double space after a period?"
    I learned to type on a teletype machine in the Navy.  A teletype message had to have two spaces after a sentence for it to be clear enough to read.  Now it's just 30 years of muscle memory.

??? question "Q24. Do you have a disclaimer? "
    Why, [yes](/about/) I do.

??? question "Q25. Where is the chat feature? "
    This site is cobbled together in my spare time and hosted on GitHub. If you would like a chat feature, feel free to file a feature request with our support team.<sup>5</sup>

??? question "Q26. Why don't footnote links work in the FAQ? "
    It's a markdown/html issue.  Trust me, it's easier this way, it's also more fun.<sup>6</sup>

??? question "Q28. Why ~~is~~ was the nav bar not in alphabetical order?"
    I have no idea.  I am pretty rigid when it comes to things like this, and I spent a good couple hours trying to figure out why it won't put things in alphabetical order and finally gave up for now.  It's definitely an [mkdocs](https://www.mkdocs.org) thing.  I'm trying to embrace being less rigid, though and this is going to be one of those times where I am going to stop fighting it and see where it goes.  Does it really need to be a meticulously trimmed garden or can it wander?  For now I'm going to consider it a vine that grows in my [garden](/) and sometimes it will grow to the directions it wants.

    Update 2022-08-13: I figured it out, the issue is that mkdocs goes by filename and not description or title of the post.  So even if my post is called "foo", if I name the file "zebra.md", it will show up at the bottom alphabetically.  While I was ok with it being weird and did finally accept it, I'm happy I figured it out.  I'm still going to fix it :)

    Update 2022-10-30: Done!

??? question "34. With different sections of the FAQ, how do you know which is the newest question?"
    Eyeball the bottom of each list, I guess.  I haven't come up with a better way just yet.

## Technology

??? question "Q12. Is there a map of the internet?"
    The Carna botnet was comprised of 420,000 devices created by an anonymous researcher to measure the extent of the Internet in what the creator called the “Internet Census of 2012”.  More details about how it went down and the resulting map can be found on [Wikipedia](https://en.wikipedia.org/wiki/Carna_botnet).

??? question "Q15. What time is it?"
    Check out the [NIST Official Official Map](https://www.time.gov/).  If you are outside the US, you're out of luck.  According to the page "The .gov means it’s official."

??? question "Q21. How do I create my own digital garden? "
    [This](https://lyz-code.github.io/blue-book/#make-your-own-digital-garden) is the place to start.  Alternatively, you can fork my repo and tinker.

??? question "Q27. How do you remove a file whose name starts with a '-'?"."
    "rm -filename" doesn't work, if you know enough about [getopt()](/tech/unix/getopts/)</a>, you can use "rm -- -filename".

??? question "Q29. What is the best distro of Linux?"
    The one *you* know best.



## Travel

??? question "Q14. Where is the best place to go for a vacation?"
    My current favorite destination is Japan.<sup>4</sup>

??? question "Q32. Why isn't [travel](/travel/) a [hobby](/hobbies/)?"
    According to Wikipedia, a hobby is considered to be a “regular activity that is done for enjoyment, typically during one’s leisure time.” Now, while traveling can be done for enjoyment, it isn’t a *regular* activity for most people. Personally, I consider it a lifestyle. 



[^Q00]: [Q00] To reach our support team, please use the chat feature.
[^Q03]: [Q03] From Hitchhiker's Guide to the Galaxy by Douglas Adams.
[^Q13]: [Q13] I started out as a dog person, but I've had good luck with cats.
[^Q14]: [Q14] I haven't been *everywhere* yet.
[^Q25]: [Q25] See footnote for Q00 above.
[^Q26]: [Q26] Fun, as in, not my problem.
[^Q30]: [Q30] I've picked a Master Lock #3 -> #6 and a few others.  Best thing to do while on a long call!
