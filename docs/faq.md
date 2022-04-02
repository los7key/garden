---
layout: page
title: FAQ
---
<script>
document.addEventListener("DOMContentLoaded", function(event) { 


var acc = document.getElementsByClassName("accordion");
var panel = document.getElementsByClassName('panel');

for (var i = 0; i < acc.length; i++) {
    acc[i].onclick = function() {
        var setClasses = !this.classList.contains('active');
        setClass(acc, 'active', 'remove');
        setClass(panel, 'show', 'remove');

        if (setClasses) {
            this.classList.toggle("active");
            this.nextElementSibling.classList.toggle("show");
        }
    }
}

function setClass(els, className, fnName) {
    for (var i = 0; i < els.length; i++) {
        els[i].classList[fnName](className);
    }
}

});
</script>

Really.  There are questions that need to be answered.  This is a work in
progress.


<p class="accordion">Q1. Do you really need an FAQ page?</p>
<div class="panel">No, but I love FAQs!  Also, the <a href="/">Introduction</a> doesn't cover everything.</div>

<p class="accordion">Q2. Who are you?</p>
<div class="panel">I'm a security enthusiast, sysadmin, veteran, father, husband, and all around geek. A jack of all trades (and master of none).</div>

<p class="accordion">Q3. What is the answer to life, the universe and everything?</p>
<div class="panel">42.</div>

<p class="accordion">Q4. Don't you have anything better to do with your time?</p>
<div class="panel">What is a better use of my time other than giving my unwanted opinion?</div>

<p class="accordion">Q5. How often will there be a new post?</p>
<div class="panel">When the mood strikes me.</div>

<p class="accordion">Q6. How long should you wait to go into the water after you've eaten?</p>
<div class="panel">At least 30 minutes.</div>

<p class="accordion">Q7. What kind of music do you like?</p>
<div class="panel">Depends on my mood and who I'm with.  Pretty much anything but country.</div>

<p class="accordion">Q8. What's wrong with country music?</p>
<div class="panel">So many things. I've tried to like it. I've worked with people that
listen to nothing but country. It's just not my thing.</div>

<p class="accordion">Q9. Why is the sky blue?</p>
<div class="panel">Sunlight reaches Earth's atmosphere and is scattered in all directions
by all the gases and particles in the air. Blue light is scattered more
than the other colors because it travels as shorter, smaller waves.</div>

<p class="accordion">Q10. What is the definition of a will?</p>
<div class="panel">A dead giveaway.</div>

<p class="accordion">Q11. How much Red Bull can someone drink and not die?</p>
<div class="panel">According to <a href="https://www.caffeineinformer.com/death-by-caffeine">Caffiene Calculator</a> I can drink 170 cans and still be safe.  Although, I'd probably be pretty sick.</div>

<p class="accordion">Q12. Is there a map of the internet?</p>
<div class="panel">The Carna botnet was comprised of 420,000 devices created by an anonymous researcher to measure the extent of the Internet in what the creator called the “Internet Census of 2012”.  More details about how it went down and the resulting map can be found on <a href="https://en.wikipedia.org/wiki/Carna_botnet">Wikipedia</a></div>

<p class="accordion">Q13. Cats or dogs?</p>
<div class="panel">Cats.</div>

<p class="accordion">Q14. Where is the best place to go for a vacation?</p>
<div class="panel">My current favorite destination is Japan.  However, that is subject to change since I haven't been everywhere yet.</div>

<p class="accordion">Q15. What time is it?</p>
<div class="panel">Check out the <a href="https://www.time.gov/">NIST Official Official Map.</a>  If you are outside the US, you're out of luck.  According to the page "The .gov means it’s official."</div>

<p class="accordion">Q16. If milk goes bad if not refrigerated, why does it not go bad inside the cow?</p>
<div class="panel">It won't go bad per se, but if a cow is not milked regularly, it can eventually stop production.</div>

<p class="accordion">Q17. Are you an expert on cows?</p>
<div class="panel">No.</div>

<p class="accordion">Q18. What about cats? </p>
<div class="panel">Not really.</div>

<p class="accordion">Q19. Why is this place called "Cat Elevator"?</p>
<div class="panel">One day I was picking up my cat and the name just came to me.  Seemed like a good fit.</div>