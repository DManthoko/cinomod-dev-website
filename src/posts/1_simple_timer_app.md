---
title: Creating a simple timer application
description: Describing I went about building a basic timer application
date: 2022-07-31
tags:
  - HTML
  - JavaScript
layout: layouts/post.njk
---

In this post, I will discuss a few points about a simple timer application that I created. It is written in HTML and Vanilla JavaScript. 

The source code can be found [here](https://github.com/cinomodev/cinomod-dev-projects/tree/main/1_simple_timer_app/version_1).

Let's get into discussing the source code. Below, you will see a snippet of the body of the index.html file.

```html
<div id="timerApp">
    <div id="countDownTimer" hidden>
    </div>
    
    <div id="countDownTimerDetails">
        <p>
          Specify a duration in the format hh:mm:ss
        </p>

        <textarea id="duration"></textarea>

        <button onclick="startTimer()">
          Start Countdown
        </button>
    </div>
</div>
```

Within the div with id ***countDownTimerDetails***, this is where I setup what is needed to get the countdown duration from the user. With the current version of the simple timer app:

- The text in the \<p\> informs the user what format to use when specifying a duration
- The duration needs to be specified inside the textarea field
- Once a user has entered a duration, they would then select the ***Start Countdown*** button. This will trigger a startTimer function, which I have defined in a separate script.js file.

After getting the duration, the startTimer() function would remove the hidden tag from ***countDownTimer***. This is where the timer would be seen. Once the countdown has been provided by the user, there is no longer any need to keep the textarea field. With that in mind, the startTimer() would add the hidden tag to ***countDownTimerDetails***. 


The countdown duration is taken in the form **hh:mm:ss**. This is then converted to seconds. The calculation is quite simple. There are 60 seconds in a minute and 3600 seconds in a hour. To convert hh:mm:ss to seconds, the *hh* value is multiplied by 3600 (60^2) and the *mm* value is multiplied by 60. *ss* is already in seconds, thus, this value is taken as is.

Converting the duration to seconds makes it simpler to handle in code. But the duration still needs to presented in the form **hh:mm:ss** to the user. I adapted the code seen in the W3Schools [JavaScript Countdown Timer](https://www.w3schools.com/howto/howto_js_countdown.asp) example to suit my needs. In the W3Schools example, the countdown duration is counted in milliseconds. In my case, I am using seconds, thus, I updated the hours, minutes and seconds calculations to look like so:

```javascript
/**
 * 
 * Converts seconds to hours, minutes and seconds
 * 
 * @param {number} countDownDuration Amount of seconds still remaining in the countdown
 * @return {string} duration A string the format hh:mm:ss
 */
function getTime(countDownDuration){
    const hours = Math.floor((countDownDuration % (60 * 60 * 24)) / (60 * 60));
    const minutes = Math.floor((countDownDuration % (60 * 60)) / (60));
    const seconds = Math.floor((countDownDuration % (60)));

    return hours + ":" + minutes + ":" + seconds;
}
```

Let's say you enter the countdown duration as 02:40:50 (2 hours, 40 minutes and 50 seconds).

The countdown duration is seconds would be:

```txt
2 hours    = 7200 seconds
40 minutes = 2400 seconds
50 seconds =   50 seconds
             
Total  = 9650 seconds
```

60 * 60 * 24 is 86400. The remainder of 9650 divided by 86400 would be 9650. 9650 divided by 60*60 is roughly 2.68. The floor of this is two. 

The remainder of 9650/3600 from the previous calculation is 2450 seconds. To convert this value minutes, divide by 60 and take the floor of the returned value.

To get the number of seconds remaining, you would only need to get the remainder when dividing the countdown duration with 60. 
