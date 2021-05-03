# Alexa-Stuff

![Alexa Icon](/Images/Amazon_Alexa_logo_115x790.svg)

As a game developer, I've experimented with TTS (Text to Speech) systems such as
[Festival](http://www.cstr.ed.ac.uk/projects/festival/) to produce game dialogue.

Achieving natural-sounding results is a lot of work. Good voice actors are expensive,
and for good reason. A lot of work is required. TTS systems are not as much work, but
the results are not anywhere near as realistic either (generally placeholder quality
only). For instance, while it is possible to get better results, the following link
is an indication of the average quality of a [Festival TTS Voice](/Voices/gen_fest.wav).

Alexa is impressive. While the regional voices vary in quality, they all sound fairly
natural - with little of the robotic quality often found with TTS systems.

Human–computer interaction (once referred to as __HCI__) is a very old research topic.
Likewise, interactive voice response or [IVR](http://en.wikipedia.org/wiki/Interactive_voice_response)
has been on the technology horizon for quite some time too. With Alexa and other similiar
products the promise of all of this research has finally reached maturity (which doesn't
mean to say that further improvement is not possible - in fact, I am sure all of these
products will continue to evolve and improve). What has finally been delivered is a
fully-fledged __VUI__ ([Voice User Interface](http://developer.amazon.com/alexa-skills-kit/vui))
with no keys to press or buttons to push; simply talk to it! Or in other words, a nice
hands-free option - which is great for preventing distracted drivers.

You can check out my first published Alexa Skill (Word Scramble) here:

    http://www.amazon.com/dp/B078WGVWL2

Or my latest Skill (Peanut Allergy Facts):

    http://www.amazon.com/dp/B07GB4BG4K

Also in French (Faits sur l'allergie aux arachides):

    http://www.amazon.fr/dp/B07GB4BG4K

And now in Spanish (Hechos de la alergia al maní):

    http://www.amazon.es/dp/B07GB4BG4K

## Contents

* [NLP](#nlp)
* [Hardware](#hardware)
    * [Router configuration](#router-configuration)
    * [App versus Web interface](#app-versus-web-interface)
    * [Wake Word](#wake-word)
    * [Volume](#volume)
    * [Languages](#languages)
        * [French](#french)
        * [Spanish](#spanish)
* [So what's it good for?](#so-whats-it-good-for)
    * [Alarms](#alarms)
    * [As a reference](#as-a-reference)
    * [As a sleep aid](#as-a-sleep-aid)
    * [Wikipedia](#wikipedia)
* [Bits and bobs of stuff for Alexa development](#bits-and-bobs-of-stuff-for-alexa-development)
    * [Alexa-hosted Skills](#alexa-hosted-skills)
    * [Node.js 8](#nodejs-8)
    * [Trivia](#trivia)
    * [Glossary](#glossary)
    * [Types of Skills](#types-of-skills)
    * [CanFulfillIntentRequest](#canfulfillintentrequest)
    * [SessionEndedRequest](#sessionendedrequest)
    * [Alexa Intents](#alexa-intents)
    * [Alexa Slots](#alexa-slots)
    * [Memory Usage](#memory-usage)
    * [Testing](#testing)
    * [Logging](#logging)
    * [Account Linking](#account-linking)
    * [Permissions](#permissions)
    * [Endpoints](#endpoints)
    * [Routing](#routing)
* [Publishing, operations and the competition](#publishing-operations-and-the-competition)
    * [Certification](#certification)
    * [Monitoring and Versioning](#monitoring-and-versioning)
    * [Commercialization](#commercialization)
    * [Swag](#swag)
    * [Alexa versus Google’s Assistant](#alexa-versus-googles-assistant)
* [UX for Voice](#ux-for-voice)
* [Privacy](#privacy)
    * [medium.com](#mediumcom)
    * [bloomberg.com](#bloombergcom)
    * [wired.com](#wiredcom)
* [Ethics](#ethics)
* [Alexa in the media](#alexa-in-the-media)
* [Icons](#icons)
* [Python](#python)
* [To Do](#to-do)

## NLP

If you're here because you are interested in natural language processing (NLP),
may I suggest you check out my [Speech Recognition](http://github.com/mramshaw/Speech-Recognition)
repo instead? Here I am mostly focussed on Alexa __devices__ and being an
__Alexa developer__. It is possible to use an Alexa SDK for NLP but I have
no knowledge of this, sorry.

## Hardware

Some general notes on actually *using* an Alexa device. If you haven't got a
Wi-Fi router, you will need one - preferably one that does G/N. And if you are planning
on using the web interface, you will need a Wi-Fi card (to talk to the Alexa device).

#### Router configuration

![Router-setup](/Images/Router_setup.png)

Set your router to use WPA or WPA2 (the _personal_ edition; I don't believe Alexa supports
the _professional_ edition as yet. And WPA2 is probably the better option here) but most
definitely __not__ WPA/WPA2. If you are really having problems or just want to get started
quickly (please re-configure later) use __None__.

Set the cipher type to __AES__ unless you are using __None__ (but probably even then too).

Amazon could really have done a much better job on this; by default I think most routers
are set to negotiate WPA/WPA2 and TKIP/AES - and Alexa devices will __not__ work if your
router is set this way.

#### App versus Web interface

I was pleased to find that - while an app is probably the way to go - it is entirely
possible to set up and configure your Alexa device via the web interface (you will need
an Amazon account, also a Wi-Fi card) available at:

    http://echo.amazon.com

[This link will redirect.]

As long as you have Wi-Fi enabled, the Alexa device will do a good job of connecting.

You will need to configure the Alexa device to use a ___permanent___ Wi-Fi connection;
once you have set it up (and registered it to your account) it will download some new
software that will allow it to use Bluetooth or pair to a device.

#### Wake Word

In the phrase:

    "Alexa, tell me something"

The word `Alexa` is what is called a __wake word__, in other words the trigger for your
device.

To change it to something else, either open up the Alexa app on your device and change it
there or else head to [echo.amazon.com](http://echo.amazon.com), sign in (you will need an
Amazon account), and use the __Settings__ panel to change it.

The choices are currently __Alexa__, __Amazon__, __Echo__ and __Computer__.

#### Volume

Alexa devices have `+` and `-` buttons to adjust the volume.

Of course, this can just as easily be done via voice:

    "Alexa, volume 6"

And:

    "Alexa, what volume are you set at?"

Also, there are `louder` and `quieter` commands too.

#### Languages

Alexa devices have always supported English but now (since March 2018) support other languages:

    http://developer.amazon.com/docs/custom-skills/develop-skills-in-multiple-languages.html

However, developing for languages other than English still seems a little problematic.

Language configuration is at the Alexa device level, so it is possible to have different Alexa
devices converse in different languages - for instance English AND French (but it will perhaps
be a good idea to have them respond to different [wake words](#wake-word) so as to save any
confusion).

##### French

For example, the
[French](http://developer.amazon.com/blogs/alexa/post/eaad8183-585e-4e6c-897d-8710d94b121f/how-to-update-your-skills-for-france)
deployment instructions. On the other hand, from the standpoint of quality, Alexa's French
voice is far better than any of Alexa's English voices.

When you submit your skill for certification, the French copy will be carefully vetted for
typos and grammatical errors. Any errors will result in a certification failure.

Check out the French version of my Peanut Allergy Facts skill (Faits sur l'allergie aux arachides):

    http://www.amazon.fr/dp/B07GB4BG4K

Interestingly, for addressing Alexa devices Amazon prefer the familiar ___tu___ form over the
more formal ___vous___ form. Using ___vous___ forms in either the launch phrases or the skill
copy will result in the skill being rejected.

There can be some trivial certification failures, which seem to be Amazon protecting its
brand. For instance, they prefer the word "skill" to "compétence" (which is probably more
correct).

UPDATE: As of October 10, 2018 Amazon announced support for
[French-Canadian French](https://developer.amazon.com/blogs/alexa/post/9fbab4e0-a4ad-4116-8810-84590e04f762/alexa-skills-kit-expands-to-include-canadian-french)
(`fr-CA` as opposed to `fr-FR`). The
[developer instructions](https://developer.amazon.com/blogs/alexa/post/a35a1a38-07fd-4d38-a99c-8d7a3f0be34b/how-to-update-your-alexa-skills-for-french-speakers-in-canada)
indicate that this may involve using a new `i18n` module.

FURTHER UPDATE: As of March 21, 2019 Amazon have released a new voice model for French-Canadian French.
It seems that there are some substantial differences that required training a unique voice model, as reported
by the [CBC](http://www.cbc.ca/news/canada/montreal/alexa-learns-quebec-french-1.5078881). In the email
I received from Amazon on March 22nd, they refer to "Canadian-French" - but the required language setting
remains `French (Canada)`. In my opinion the French-Canadian voice and model far exceed any of the English
equivalents (and so are on par with the original French voice and model) but your mileage may vary.

##### Spanish

Alexa has voices for Spanish, both for es-ES (Spain) and es-MX (Mexico).

As with [French](#french), Amazon prefer the familiar ___tú___ form over the more formal ___usted___ form.
Use of the formal forms in either the launch phrases or the skill copy will result in the skill being rejected.

To my ear, neither of these Spanish voices is of the same quality as the French voices, but that may be
a personal thing.

Check out the Spanish version of my Peanut Allergy Facts skill (Hechos de la alergia al maní):

    http://www.amazon.es/dp/B07GB4BG4K

## So what's it good for?

It's a little too early for me to say, but if you're single (Honey, I had a dream you were
talking to some woman named Alexa ?!?!) it probably makes a good bedside radio/alarm clock.

UPDATE: As of September, 2018 there is talk of a `whisper` recognition mode (as far as I
know, SSML has always supported a whisper mode for Alexa utterances).

    http://developer.amazon.com/blogs/alexa/post/c0e7798d-32bc-4549-9c24-97d204a7bf3a/whisper-to-alexa-and-she-ll-whisper-back

> (The U.S. English version will be available in October.)

Most of the following can also be done from a mobile phone, which is only slightly more
inconvenient than speaking to an Alexa device. Using an Alexa device is almost always a
hands-free operation - which is generally a little more convenient. On the other hand,
Alexa will ___only___ respond to a [wake word](#wake-word) whereas a mobile phone can be
very susceptible to room noise and chatter (but does not need a wake word).

#### Alarms

For instance:

    "Alexa, set an alarm for 5 minutes"

    "Five minutes, starting now"

    [Five minutes passes.]

    [Alexa devices chimes.]

    "Alexa, cancel the alarm." [Or you could press the wake button.]

Timers and alarms can be named, and you can have up to 100 of them.

Apparently they do not depend on the cloud either, being device-resident.

To hear what alarms are set:

    "Alexa, what alarms have been set?"

["No alarm has been set."]

#### As a reference

For those hard-to-spell words:

    "Alexa, how do you spell Wikipedia?"

[She also knows weights and measures too.]

#### As a sleep aid

If you are having trouble sleeping:

    "Alexa, open Rain Sounds"

[There are far too many of these to be specific, but you can probably find one you like.]

If you pair Alexa to your smartphone, she can dial numbers for you (but your
smartphone could probably already do this).

#### Wikipedia

Perhaps my favourite skill:

    "Alexa, Wikipedia: Hanoi"

[She gives the first paragraph or so; you can ask for more if you wish.]

## Bits and bobs of stuff for Alexa development

Now follows some random stuff loosely oriented around being an Alexa developer.

#### Alexa-hosted Skills

Amazon now offers a beta version of
[Alexa-hosted Skills](http://developer.amazon.com/docs/hosted-skills/build-a-skill-end-to-end-using-an-alexa-hosted-skill.html)
which can greatly simplify the development and deployment process. It doesn't even
require an AWS account! [But it is limited to the [free tier](http://aws.amazon.com/free/)
options and limitations.]

Caveats: only __Node.js version 8__ is supported at present; and session data has
changed (if I read things aright) from DynamoDB persistence to S3 persistence.

In my opinion Amazon has greatly simplified the initial coding experience, making
Alexa Skills a great deal more accessible to beginners. What is not clear to me is
how easy it might be to migrate test code into a production environment.

For my purposes I will be sticking with my established methods - and will not be
writing Alexa-hosted Skills.

[UPDATE: there is a "Promote to live" button for Alexa-hosted Skills which I missed.
 It may very well be that Amazon handles the test -> production migration, although
 I still need to check this out.]

The Amazon (and Alexa) developer experience continues to evolve by leaps and bounds.
While I have not always been a fan of some of their "improvements" I have to say
that I am a fan of ___Lambda Layers___ (released November 2018), which you can read
about here:

    http://aws.amazon.com/about-aws/whats-new/2018/11/aws-lambda-now-supports-custom-runtimes-and-layers/

You can find the developer documentation here:

    http://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html

I am currently considering updating all of my Node.js functions from Node.js 6
to Node.js 8, so the following feature may well save me some work:

> Lambda Layers are a new type of artifact that can contain arbitrary code and data,
> and may be referenced by zero, one, or more functions at the same time. Lambda
> functions in a serverless application typically share common dependencies such as
> SDKs, frameworks, and now runtimes. With layers, you can centrally manage common
> components across multiple functions enabling better code reuse. To use layers,
> you simply put your common code in a zip file, and upload it to Lambda as a layer.
> You then configure your functions to reference it.

As this will enable me to provision and/or update a single Node.js runtime, I
really think this is a very welcome improvement over the current situation (of
having separate runtimes for each Lambda function).

As it will __also__ enable AWS console editing of the source code of my Lambda
functions, I think this is a big win.

Considering the hazy documentation about Alexa-hosted Skills (which are still
a beta offering) I think separate back-end Lambda functions (along with perhaps
a common Lambda Layer) will continue to be my preferred arctitecture.

#### Node.js 8

Although there are many language options in terms of writing Lambda functions, in
my opinion __Node.js__ is possibly the best choice at present - both for example
code and support from the AWS Lambda functions dashboard.

Amazon announced Node.js version 8 on April 2nd, 2018:

   http://aws.amazon.com/blogs/compute/node-js-8-10-runtime-now-available-in-aws-lambda/

One problem with coding in the Cloud is the necessity to upgrade software according
to a Cloud Provider's timetable. For instance, I received an email from Amazon on
March 24th 2019 warning me that __Node.js version 6__ would be declared End-of-Life
(EOL) on April 2019 (this can be as simple as selecting a different Node.js runtime).
[I also received a follow-up email on April 16th. Kudos to Amazon.]

As Node.js has the largest attack surface and greatest number of exploits of any
modern language, this is actually good news. The roll-out is not too bad either:
slightly more than 30 days (actually 30 days plus a week) warning of the stopping
of Node.js 6 activation (April 30) and then 30 days more before Node.js is fully
shelved (May 30).

[The above only applies to AWS Lambda functions.]

Amazon provides some background on why upgrading to Node.js version 8 is a good idea:

    http://aws.amazon.com/blogs/compute/node-js-8-10-runtime-now-available-in-aws-lambda/

[Well worth a read. __TL;DR__ Node.js 8 features ___async/await___ which really simplifies promises.]

#### Trivia

There are Easter Eggs in Alexa:

    "Alexa, cheer me up."

    "Alexa, tell me a story."

    "Alexa, what's on your mind?"

    "Alexa, tell me something."

For instance, according to Alexa:

    The word 'boredom' was first coined by Charles Dickens in his 1852 novel Bleak House.

So in a way, boredom was __invented__ by Charles Dickens. This may not come as a surprise
to anyone who has ever been required to read one of his very lengthy works!

[This is not a knock on Dickens: I have actually read Bleak House - and I wasn't required
to do so, so I guess I was reading for pleasure. My point is that actually requiring anyone
to read ___anything___ is probably a good way to make sure they don't enjoy the experience.
A better route to go is to ___ban___ the book; our library had a week of banned books
once - and I was very surprised to find that I had aleady read at least half of them.
`Of Mice and Men`, `The Adventures of Tom Sawyer`, `Adventures of Huckleberry Finn` or
`The Catcher in the Rye`, anyone? Recently I very much enjoyed `The Curious Incident of
the Dog in the Night-Time` (recommended by a librarian). All, at one time or another,
banned. It seems that pretty much everything that is worth reading has been banned at
one time or another.]

#### Glossary

As is usually the case, probably the best place to start is by defining terms or establishing
a vocabulary (sometimes called a Domain-Specific Language or __DSL__). For instance, rather
than the over-used __app__, Alexa developers write __skills__ (but some of the AWS documentation
stills discusses skills as if they were apps). The Alexa glossary is actually pretty good
(also brief) and well worth reading:

    http://developer.amazon.com/docs/ask-overviews/alexa-skills-kit-glossary.html

[As is usually the case, things change quickly in the cloud and the documentation does not
always keep pace. For instance, as I write this, [Golang](http://github.com/mramshaw/Golang)
is not listed in this Glossary as an option for AWS Lambda functions - and Amazon recently
added support for Go to Lambda functions. ___Caveat emptor___.]

For a broader view of things (i.e. not just AWS), check out:

    http://www.witlingo.com/voice-first-glossary-of-terms/

#### Types of Skills

There are various skill types. The main focus here so far has been
[Custom Skills](http://developer.amazon.com/docs/custom-skills/understanding-custom-skills.html),
although 
[Flash Briefings](http://developer.amazon.com/docs/flashbriefing/understand-the-flash-briefing-skill-api.html)
(which allow for RSS or JSON feeds) also look pretty interesting. Although getting these to ___pause___ or
___stop___ seems to be a little tricky.

#### CanFulfillIntentRequest

In the case where a user does not know the specific __name__ for a skill, this new beta
offering allows Amazon to select a set of skills that _might_ fulfill the request:

    http://developer.amazon.com/docs/custom-skills/understand-name-free-interaction-for-custom-skills.html

Currently in beta (as of August 2018), and US-only.

#### SessionEndedRequest

This indicates an abnormal end of the current session, most probably a user timeout.

For more information:

    http://developer.amazon.com/docs/custom-skills/handle-requests-sent-by-alexa.html#sessionendedrequest

Nota bene:

> Your service cannot send back a response to a `SessionEndedRequest`.

For even more information:

    http://developer.amazon.com/docs/custom-skills/request-types-reference.html#sessionendedrequest

[Provides details of the various reasons why the session ended.]

#### Alexa Intents

While Alexa provides some very useful
[Standard Built-in Intents](http://developer.amazon.com/docs/custom-skills/standard-built-in-intents.html#available-standard-built-in-intents)
it may be a good idea to extend them with Standard Utterances as follows:

    AMAZON.RepeatIntent please repeat
    AMAZON.YesIntent okay

If the __Audio Player__ option is checked, AMAZON.PauseIntent and AMAZON.ResumeIntent
must be specified. Note that these refer to ___streaming___ audio, not normal audio
such as attending or playback - which will both function correctly without the Audio
Player option specified.

For a good example of how __not__ to implement an audio-playing interface, try:

    "Alexa, tell me something inspiring"

[Neither "Pause" nor "Resume" seem to work correctly.]

UPDATE: As of April, 2018 this skill seems to have been withdrawn.

    "Sorry, I don't know that one."

[This seems to be what she says whenever she doesn't understand your question.]

#### Alexa Slots

It's a good idea to check up on the
[defined Alexa slots](https://developer.amazon.com/docs/custom-skills/slot-type-reference.html)
when considering a voice interaction. Using a predefined slot may well save both you and
your users some frustration while getting to grips with using Alexa. The defined slots are
mainly oriented to the Amazon shopping experience, but some of them may well be useful to
Alexa developers. They add new
[List Slot Types](http://developer.amazon.com/docs/custom-skills/slot-type-reference.html#list-slot-types)
from time to time (such as `AMAZON.Animal`), so it's worth checking back periodically.
Be careful not to use any slot types marked as __Public beta__.

While Alexa has some very useful built-in slots, it's probably a 'best practice' to define
custom slots. For one thing, the built-in slots are extensive and it is probably a good
idea to restrict these quite a bit. Follow the following link for some useful tips on
[formatting slot values](http://developer.amazon.com/docs/custom-skills/define-the-interaction-model-in-json-and-text.html#cert-custom-slot-types).

#### Memory Usage

The smallest possible allocation for a Lambda function is 128 MB. So it is a good idea to
use this as a target, rather than trying to minimize memory usage with procedural code.

#### Testing

Rigorous manual testing is of course a first step, but what about automated testing?

Amazon provides a good summary of the various testing options:
[Why testing and automation matter](http://developer.amazon.com/blogs/alexa/post/e2f3d18c-13ca-4796-bc83-e8a196f20e57/building-engaging-alexa-skills-why-testing-and-automation-matter).

One interesting quote from the above article:

> we may not be aware of any problems until a user writes a one-star review.

The [Bespoken](http://docs.bespoken.io/en/latest/) testing framework is well worth a look:

    http://docs.bespoken.io/en/latest/getting_started/

Alexa:

    http://docs.bespoken.io/en/latest/tutorials/tutorial_alexa_unit_testing/

SDK:

    http://github.com/bespoken/virtual-device-sdk

Example:

    http://github.com/bespoken/GuessThePrice

And:

    http://bespoken.io/blog/automated-testing-for-alexa-skills-2/

For monitoring your skills in production, logging (see the next section) is essential.

Amazon Cloudwatch alerts can be set to go off if any unexpected circumstances or events arise.

#### Logging

Each invocation (request or reponse) of a Lambda function will generate billing details,
consisting of three [CloudWatch](http://docs.aws.amazon.com/lambda/latest/dg/monitoring-functions.html)
events (a START event, an END event, and a REPORT event). These may be filtered out
of the CloudWatch console by typing:

    -START -END -REPORT

into the `Filter events` text box (sadly these must be typed in __each and every__ time;
a better way to do this is to use CloudWatch Logs Insights and then create a custom
 __Cloudwatch Dashboard__).

Amazon published a useful blog post on November 27, 2018 introducing Cloudwatch Logs Insights:

    http://aws.amazon.com/blogs/aws/new-amazon-cloudwatch-logs-insights-fast-interactive-log-analytics/

[Note that Cloudwatch Logs Insights will incur usage charges based upon the amount of log data.]

Amazon provides useful query examples, both in the Cloudwatch Insights console as well as at:

    http://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_QuerySyntax-examples.html

The following code can be used to filter out billing details:

```
fields @message |
filter @type != "REPORT"
 and @type != "START"
 and @type != "END"
```

The following code can be used to only show exceptions:

```
fields @message |
filter @message like /Exception/
```

In my experience CloudWatch Logs Insights includes deleted log entries.

Due to the voluminous billing details, the urge to log each and every interesting user
interaction is probably to be avoided. Even so, for debugging reasons it is important to
log every __significant__ event (user responses, unhandled events, enough life cycle events
for context). There is a rich market for logging analysis, which should be a warning to
be careful about what gets logged - for privacy reasons, if not just to reduce clutter.

Of course, it is entirely possible to create a simple skill (such as a Facts skill) that
does not require debugging, in which case the performance statistics available from the
[AWS Lambda console](http://console.aws.amazon.com/lambda/) may be sufficient.

#### Account Linking

This refers to linking to an external (i.e. non-Amazon) account. It looks like standard OAuth.

#### Permissions

This refers to linking to an Amazon account. There are two groups: location (self-explanatory)
and lists. Alexa customers have two default lists: __to-do__ and __shopping__. Access to these
seems to be standard REST. There are two permissions: __read__ and __write__. Requests are throttled.
Follow the link for the
[Permissions API](http://developer.amazon.com/docs/custom-skills/access-the-alexa-shopping-and-to-do-lists.html#list-management-quick-reference).

#### Endpoints

For the purposes of providing content distribution, the region mappings are as follows:

Alexa Developer Console|Region|AWS internal region|Shows in AWS Console as
-----------------------|------|-------------------|-----------------------
Default|US West (Oregon)|us-west-2|Oregon
North America|US East (N. Virginia)|us-east-1|N. Virginia
Europe and India|EU (Ireland)|eu-west-1|Ireland
Far East|Asia-Pacific (Tokyo)|ap-northeast-1|Tokyo

[The `Endpoints` panel on the Alexa Developer Console provides popups that show recommendations.
 You are limited to regions that provide Lambda functions (initially only North Virginia) - here
 I have chosen to make my default region Oregon (i.e. on the West Coast) for content distribution
 purposes but North Virginia might be a better choice. UPDATE: With all of the endpoints specified
 the default endpoint does not seem to ever be invoked - or at least that has been my experience.]

Bear in mind that any needed ancillary resources (S3, DynamoDB tables) must also be duplicated
to all appropriate regions. For databases, the thorny issue of whether or not to replicate the
databases across regions needs to be considered (for DynamoDB this might be as simple as using a
[DynamoDB Global Table](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GlobalTables.html)).

Interestingly enough, IAM permissions are the exception as they are __Global__ (i.e. apply to
all regions). Following security best practices such as the
[Principle of least privilege](http://en.wikipedia.org/wiki/Principle_of_least_privilege),
this means provisioning and allocating separate IAM policies and roles for each region.

[Cloudwatch Dashboards are also Global, so that once defined they are available in all regions.]

With some jiggery-pokery, the Endpoints panel can be used to test each and every Lambda function
(endpoint), but the Alexa model must be saved & rebuilt every time the endpoints are changed.

#### Routing

Language variations appear to be routed as follows:

Language|variant|Routed to
--------|-------|---------
English|en-AU|N. Virginia / Tokyo
English|en-CA|N. Virginia
English|en-GB|N. Virginia / Ireland
English|en-IN|N. Virginia / Ireland
English|en-US|N. Virginia
French|fr-CA|N. Virginia
French|fr-FR|Ireland
Spanish|es-MX|N. Virginia
Spanish|es-SP|Ireland

[Sorted alphabetically]

## Publishing, operations and the competition

#### Certification

Once your Alexa skill is complete, you can submit it for certification. Amazon posts a
certification results ETA on their developer console.

It's worth checking the certification requirements very carefully before submitting a skill.
Amazon will cross-reference these if they reject your skill submission:

    http://developer.amazon.com/docs/custom-skills/voice-interface-and-user-experience-testing-for-a-custom-skill.html

They can - and apparently _will_ - reject a skill for fairly arbitrary reasons, for instance
if it _might_ compete with their __Audible.com__ business. And they seem to be prone to
changing the rules to suit themselves - at the moment, advertising is a no-no, but once
they figure out how to commercialize (no pun intended) it I am sure it will again become
an option.

Even so, their rejection emails are very specific and actually quite helpful - they highlight
the rejected sentences and also provide copy that they would prefer. It is worth noting that
the name of your skill must be consistent in all usages - even if this might conflict with
normal grammatical usage (think of this as "branding").

Note that certification testing for compliance is not the same thing as logic testing, which
is a developer responsibility. It's entirely possible to have a skill certified that still
has some bugs in it. There is also a __Skills Beta Testing__ program (with 500 invites) which
looks worthwhile.

Certification has gotten lengthier and more stringent over the years (which is a good thing).
It took eight calendar days to get my first Alexa skill certified. That skill, resubmitted
later with a few minor improvements, only took a day or so to get re-certified. A skill
submitted April 12, 2019 was initially scheduled for an April 30th notification - so 18 days,
or 12 business days (almost twice as long as a few years ago - but also featured 9 language
variations). The initial rejection came April 15 (so about four calendar days) - and took
issue with some French copy that had previously passed muster (along with some other things).
As VUIs (Voice User Interfaces) continue to gain acceptance, it essential that the quality
of the user experience continues to improve. [After some back and forth, the skill was in
the end certified on April 24, 2019 - however, this was a pre-existing skill to which I was
mainly adding support for [Spanish](#spanish).]

#### Monitoring and Versioning

Once your skill has been submitted for certification it will be locked on the developer console.
However, if you are using AWS Lambda functions, you can monitor the certification testing via
Cloudwatch Logs.

Once your skill has been certified (or re-certified), a new development version will automatically
be created for you.

While it may be tempting to re-use any existing Lambda functions, it is probably a better
idea to create a new Lambda function for each iteration (version) of your Alexa skill.

The Alexa developer dashboard is excellent for monitoring purposes.

#### Commercialization

[In-Skill Purchasing](http://developer.amazon.com/alexa-skills-kit/earn) is now generally available.

[Even though I was invited to join the __beta__, I still haven't looked into this so cannot comment.]

Another development to watch is [Alexa Traffic Analysis](http://www.alexa.com/siteinfo/aws.org).

[I may have mis-read this development. __Alexa.com__ proudly proclaims itself an Amazon company,
 but it may not actually have anything to do with Alexa ___devices___.]

Good demographic data for Alexa is hard to come by, this is all I could find:

    http://www.slideshare.net/stevelsilver/amazon-echo-alexa-demographics-75193964

[Published on Apr 19, 2017]

#### Swag

I got an email March 8th, 2018 that my skill had had more than 100 unique customers within 30 days of publication and therefore
qualified for the January Echo Dot promotion. My free Alexa Dot showed up ___about a half-hour later___ (now that's shipping!).

Still no custom developer hoodie though. UPDATE: I got an email March 29th that my custom hoodie had been shipped.
And it eventually showed up April 2nd (it was addressed to ALEXA DEVELOPER MARTIN RAMSHAW which I thought was a nice touch).

![Swag](/Images/Swag.png)

Alexa Dot on the left, custom hoodie in the background. If you do not have a Wi-Fi router (right, not free) you will need one.

UPDATE: As of April 2019 it seems that Amazon have largely dropped free developer swag, although they still feature occasional
competitions. Google seem to be playing catch-up however, as they offer t-shirts as well as Google Home devices for qualifying
new Actions. [Both companies offer free credits, although once again Google's offering seems to be more generous.]

#### Alexa versus Google’s Assistant

[I have also looked into [Google Assistant](https://github.com/mramshaw/Google-Assistant), although not yet as deeply as Alexa.]

The first distinction to make when comparing the offerings from Amazon and Google is to differentiate between the ___software___
(i.e. the capabilities of the devices - such as `Skills` or `Actions`) and the ___hardware___ (meaning the devices themselves,
such as the `Alexa Dot` / `Alexa Echo` / `Alexa Echo Plus` / `Alexa Show` - and the `Google Home Mini` / `Google Home` /
`Google Home Hub`).

While the __devices__ largely offer much the same features (different designer colours, similiar form factors and sound quality),
differing slightly on price and aesthetics, the two offerings are somewhat different in terms of their software capabilities, but
not so much that - in this highly-charged competitive market - either offering has a significant advantage. And the situation can
only be expected to evolve (and probably rapidly, given that it's a huge market). In short, any comparisons between them must be
taken with a grain of salt, given that the situation is very fluid.

Even so, follow the link for an interesting read about
[Amazon’s Alexa vs. Google’s Assistant](http://gigaom.com/2017/06/12/amazons-alexa-vs-googles-assistant-same-questions-different-answers/).

__tl;dr__ Information is contextual and nuanced, and relying verbatim on either of these
devices is problematic. Note that the article is slightly dated, being from ___2017___.

As of the time of this writing (April 2019) Amazon is apparently leading Google with 15,000+ skills, but as the Google
Assistant features a completely different integration model and marketplace this is probably not significant. [Google
actively curates its content, so that it's actions do not need to be actively installed - unlike Alexa skills, which
need to be individually ___enabled___.]

There are extrinsic factors as well; Alexa can tie into the whole Amazon buying experience (as in: "Alexa, where are my
shipments?") - and for entertainment purposes can also tie into Amazon Prime - while Google can integrate with the entire
Google platform (as in: "What's on my calendar?" - which ties into Google Calendar).

To see available Google Actions, check out:

    http://assistant.google.com/explore

[However, be aware that these actions may not be available in all languages or all regions.]

The devices roughly correspond as follows:

Amazon|Google
------|------
Alexa Dot|Google Home Mini
Alexa Echo|Google Home
Alexa Echo Plus|no Google equivalent (as far as I know)
Alexa Show|Google Home Hub

The smallest devices are fine for voice interaction, but not so great for listening to music (although newer Alexa
Dot devices have an audio-out jack). The mid-range devices feature better speakers (and so are better for listening
to music), while the high-end devices also have display surfaces.

## UX for Voice

While Amazon provides quite a lot of content related to Alexa, sometimes an external
source may provide a broader perspective. Some of the following may be of interest:

    http://www.lynda.com/User-Experience-tutorials/UX-Voice-Planning-Implementation/679644-2.html

    http://softwareengineeringdaily.com/2018/05/18/alexa-voice-design-with-paul-cutsinger/

Note that UX for Voice is __not__ [IVR](http://en.wikipedia.org/wiki/Interactive_voice_response),
which is a much older technology.

## Privacy

There are some troubling privacy aspects to having voice devices in your household or
place of work. Here is an interesting video from Vox about some of the implications:

    http://www.youtube.com/watch?v=IUEN2TAqlmU

[The video was posted on Dec 28, 2020.]

Now that adoption of voice-activated devices has become widespread the situation
can only be expected to evolve.

One or two interesting quotes follow.

#### medium.com

From a `medium.com` article:

> We expect to enjoy privacy in our own homes, but this is ultimately incompatible
> with the reality that the data collected by your Echo belongs to Amazon, and not you.

And:

> So while virtual assistants themselves are not inherently problematic,
> they do bring to the fore many of the problems that have built up around
> our use of centralised data-driven services, and especially so for home
> Internet of Things devices.

Both from:

    http://medium.com/oxford-university/whos-storing-your-conversations-e5736fc5d9f5

#### bloomberg.com

From a `bloomberg.com` article:

> Amazon.com Inc. employs thousands of people around the world to help improve the
> Alexa digital assistant powering its line of Echo speakers. The team listens to
> voice recordings captured in Echo owners’ homes and offices. The recordings are
> transcribed, annotated and then fed back into the software as part of an effort
> to eliminate gaps in Alexa’s understanding of human speech and help it better
> respond to commands.

From:

    https://www.bloomberg.com/news/articles/2019-04-10/is-anyone-listening-to-you-on-alexa-a-global-team-reviews-audio

The article is well worth a read as it gives quite a lot of background on Amazon
and their voice training practices.

#### wired.com

It is routine to have human experts review audio snippets to ensure accurate STT transcription.

This is not without some troubling aspects:

> Google paused human audio review worldwide in July after reports that a contractor was leaking audio snippets in Dutch.

Despite the headline of the article, this is not just a Google issue.

Apple:

> About three weeks after Google paused audio snippet review, Apple did as well on August 2.

Amazon:

> Amazon ... offers the option for users to opt-out of sharing audio clips for transcription.
> The company launched a dedicated "Alexa Privacy Hub" in May and added the voice command,
> "Alexa, delete everything I said today," soon after.

Microsoft:

> Microsoft said at the end of August that it no longer uses human review for audio snippets

Facebook:

> Facebook said that it would stop human review on audio from Messenger

And:

> All the major smart assistant developers maintain that audio snippets are fully anonymized
> before they go out to reviewers and most specifically say that less than one percent of total
> interactions with smart assistants actually get reviewed by a person.

All from:

    http://www.wired.com/story/google-assistant-human-transcription-privacy/

[Wired specializes in stories about technology that are not overly technical. Well worth a read.]

## Ethics

For techies and tech companies, the ability to be able to do something has usually out-weighed ethical considerations.

[This has been a long-term trend, with science and technology generally out-pacing legal and ethical considerations.
 However, legislation can be relied upon to eventually catch up to technology. Rather than having to expensively
 retrofit privacy safeguards into an existing product strategy, it behooves innovators to behave proactively and
 consider legal and ethical concerns from the outset. This can be an effective differentation strategy, and very
 possibly an effective means of securing a competitive advantage. The end result might very possibly be a
 corporate privacy policy. And then of course there is the troubling issue of [affinity groups](http://en.wikipedia.org/wiki/Affinity_group).]

While legal considerations concern themselves with the ___law___ (and can be considered to be the minimum requirement),
ethical considerations go above and beyond and are generally concerned with ___morality___. Just because something
is __legal__ does not necessarily mean it is __moral__. While legal penalties can include fines and prohibitions,
ethical penalties can include loss of consumer confidence, goodwill, market share and revenue.

For those interested in such things, the contrasting ethical frameworks are [Deontology](http://en.wikipedia.org/wiki/Deontological_ethics)
and [Utilitarianism](http://en.wikipedia.org/wiki/Utilitarianism). Deontology is the idea that an action is either
right or wrong, and can be assessed on that basis. For instance, respecting a customer's right to privacy. Utilitarianism
is what is known as a [consequentialist theory](http://en.wikipedia.org/wiki/Consequentialism) - in that actions can be
evaluated in terms of their __consequences__ - and can broadly be categorized as ___the end justifies the means___.
For instance, the idea that the benefits of aggregating a properly-anonymized collection of user utterances outweighs
the costs of a number of violations of customer privacy (these things generally seem to be framed in terms of cost-benefit
analysis).

Just as ethics is a growing concern in the machine learning world, so it is also becoming important in the voice world,
and not simply from a [privacy](#privacy) perspective either. As the following Fortune article should make clear, failing
to take into account ethical considerations can be expensive - if not in a purely legal sense, then in a brand,
market-share or professional prestige way:

    http://fortune.com/2018/05/11/google-duplex-virtual-assistant-ethical-issues-ai-machine-learning/

> As prominent sociologist Zeynep Tufekci [put it](http://twitter.com/zeynep/status/994233568359575552):
> “Google Assistant making calls pretending to be human not only without disclosing that it’s a bot, but
> adding ‘ummm’ and ‘aaah’ to deceive the human on the other end with the room cheering it… horrifying.
> Silicon Valley is ethically lost, rudderless and has not learned a thing.”

[The above quote is from the preceding Fortune article.]

## Alexa in the media

You know Alexa is mainstream when Saturday Night Live parodies it:

    http://www.youtube.com/watch?v=YvT_gqs5ETk

Here is a UK advertisement:

    http://www.youtube.com/watch?v=sulDcHJzcB4

## Icons

Some [Gimp](http://www.gimp.org/) templates

## Python

Some sample Python code

## To Do

- [x] Investigate Alexa Demographics
- [ ] Investigate the use of [Flash Briefings](http://developer.amazon.com/docs/flashbriefing/understand-the-flash-briefing-skill-api.html)
- [x] Investigate the use of [DynamoDB](http://aws.amazon.com/dynamodb/) as a back end
- [x] Investigate the use of [Alexa Custom Slots](http://developer.amazon.com/docs/custom-skills/slot-type-reference.html)
- [x] Investigate the use of __Account Linking__ and __Permissions__
- [x] Investigate __Cloudwatch Event Logging__
- [x] Investigate __Cloudwatch Event Logging filters__
- [x] Investigate __CloudWatch Logs Insights__
- [x] Investigate __Cloudwatch Dashboards__
- [ ] Investigate __Cloudwatch Alerts__
- [ ] Investigate __CanFulfillIntentRequest__ once it comes out of Beta or becomes multi-language
- [ ] Investigate [Alexa Automated Testing](http://github.com/alexa/skill-sample-nodejs-test-automation)
- [ ] Investigate [Alexa Load Testing](http://github.com/alexa/skill-sample-node-js-build-scale-test)
- [ ] Investigate [Alexa More Intent](http://developer.amazon.com/docs/custom-skills/standard-built-in-intents.html#amazonmoreintent)
- [ ] Investigate [Alexa Testing](http://github.com/BrianMacIntosh/alexa-skill-test-framework) [looks pretty spiffy]
- [ ] Investigate [Alexa Timeouts](http://github.com/nickclaw/alexa-ability-timeout)
- [ ] Investigate [Virtual Alexa](http://github.com/bespoken/virtual-alexa) [also looks pretty spiffy]
- [x] Investigate [Alexa-hosted Skills](http://developer.amazon.com/docs/hosted-skills/build-a-skill-end-to-end-using-an-alexa-hosted-skill.html)
- [x] Investigate __SessionEndedRequest__
- [x] Investigate Internationalization (i18n) and Localization (L10n)
- [x] Investigate Alexa’s French voices
- [x] Investigate Alexa’s Spanish voices
- [x] Investigate Google’s Assistant
- [x] Investigate Google Actions
- [x] Add notes on Ethical Principles
