# Alexa-Stuff

![Alexa Icon](/Images/alexaLogo2x._V516058141_.png)

As a game developer, I've experimented with TTS (Text to Speech) systems such as
[Festival](http://www.cstr.ed.ac.uk/projects/festival/) to produce game dialogue.

Achieving natural-sounding results is a lot of work. Good voice actors are expensive,
and for good reason. A lot of work is required. TTS systems are not as much work, but
the results are not anywhere near as realistic either (generally placeholder quality
only). For instance, while it is possible to get better results, the following link
is an indication of the average quality of a [Festival TTS Voice](/Voices/gen_fest.wav).

Alexa is impressive. While the regional voices vary in quality, they all sound fairly
natural - with little of the robotic quality often found with TTS systems.

You can check out my first published Alexa Skill here:

    https://www.amazon.com/dp/B078WGVWL2

## Bits and bobs of stuff for Alexa development

#### Trivia

There are Easter Eggs in Alexa:

    "Alexa, what's on your mind?"

    "Alexa, tell me something"

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

#### Wake Word

In the phrase:

    "Alexa, tell me something"

The word `Alexa` is what is called a __wake word__, in other words the trigger for your
device.

To change it to something else, either open up the Alexa app on your device and change it
there or else head to [echo.amazon.com](echo.amazon.com), sign in (you will need an Amazon
account), and use the __Settings__ panel to change it.

#### Alexa Intents

While Alexa provides some very useful
[Standard Built-in Intents](https://developer.amazon.com/docs/custom-skills/standard-built-in-intents.html#available-standard-built-in-intents)
it may be a good idea to extend them with Standard Utterances as follows:

    AMAZON.YesIntent okay

If the __Audio Player__ option is checked, AMAZON.PauseIntent and AMAZON.ResumeIntent
must be specified. Note that these refer to ___streaming___ audio, not normal audio
such as attending or playback - which will both function correctly without the Audio
Player option specified.

For a good example of how __not__ to implement an audio-playing interface, try:

    "Alexa, tell me something inspiring"

[Neither "Pause" nor "Resume" seem to work correctly.]

#### Alexa Slots

While Alexa has some very useful built-in slots, it's probably a 'best practice' to define
custom slots. For one thing, the built-in slots are extensive and it is probably a good
idea to restrict these quite a bit. Follow the following link for some useful tips on
[formatting slot values](https://developer.amazon.com/docs/custom-skills/define-the-interaction-model-in-json-and-text.html#cert-custom-slot-types).

#### Memory Usage

The smallest possible allocation for a Lambda Function is 128 MB. So it is a good idea to
use this as a target, rather than trying to minimize memory usage with procedural code.

#### Logging

Each invocation (request or reponse) of a Lambda function will generate billing details,
consisting of three log events (a START event, an END event, and a REPORT event). These may
be filtered out by typing:

    -START -END -REPORT

into the `Filter events` text box (sadly these must be typed in __each and every__ time;
perhaps the recommended way to do this is to create a custom __Dashboard__).

Due to the voluminous billing details, the urge to log each and every interesting user
interaction is probably to be avoided. Even so, for debugging reasons it is important to
log every __significant__ event (user responses, unhandled events, enough life cycle events
for context). There is a rich market for logging analysis, which should be a warning to
be careful about what gets logged - for privacy reasons, if not just to reduce clutter.

#### Account Linking

This refers to linking to an external (i.e. non-Amazon) account. It looks like standard OAuth.

#### Permissions

This refers to linking to an Amazon account. There are two groups: location (self-explanatory)
and lists. Alexa customers have two default lists: __to-do__ and __shopping__. Access to these
seems to be standard REST. There are two permissions: __read__ and __write__. Requests are throttled.
Follow the link for the
[Permissions API](https://developer.amazon.com/docs/custom-skills/access-the-alexa-shopping-and-to-do-lists.html#list-management-quick-reference).

#### Certification

Once your Alexa skill is complete, you can choose to submit it for certification. I _thought_
this would take up to five days (so basically a calendar week) as I am sure I read this in
their documentation somewhere - but, as often happens with AWS documentation, I cannot find
any reference to this now.

It's worth checking the certification requirements very carefully before submitting a skill.

They can - and apparently _will_ - reject a skill for fairly arbitrary reasons, for instance
if it _might_ compete with their __Audible.com__ business. And they seem to be prone to
changing the rules to suit themselves - at the moment, advertising is a no-no, but once
they figure out how to commercialize (no pun intended) it I am sure it will again become
an option.

[It took eight calendar days to get my first Alexa skill certified.]

#### Monitoring and Versioning

Once your skill has been submitted for certification it will be locked on the developer console.
However, if you are using AWS Lambda functions, you can monitor the certification testing via
Cloudwatch Logs.

Once your skill has been certified, a new development version will automatically be created.

While it may be tempting to re-use any existing Lambda functions, it is probably a better
idea to create a new Lambda function for each iteration (version) of your Alexa skill.

The Alexa dashboard is excellent for monitoring purposes.

#### Commercialization

There is a beta available for [In-Skill Purchasing](https://developer.amazon.com/alexa-skills-kit/earn).

Another development to watch is [Alexa Traffic Analysis](https://www.alexa.com/siteinfo/aws.org).

#### Alexa versus Google’s Assistant

Follow the link for an interesting read about
[Amazon’s Alexa vs. Google’s Assistant](https://gigaom.com/2017/06/12/amazons-alexa-vs-googles-assistant-same-questions-different-answers/).

__tl;dr__ Information is contextual and nuanced, and relying verbatim on either of these
devices is problematic.

#### Icons

Some [Gimp](https://www.gimp.org/) templates

#### Python

Some sample Python code

#### To Do

- [x] Investigate the use of [DynamoDB](https://aws.amazon.com/dynamodb/) as a back end
- [x] Investigate the use of [Alexa Custom Slots](https://developer.amazon.com/docs/custom-skills/slot-type-reference.html)
- [x] Investigate the use of __Account Linking__ and __Permissions__
- [x] Investigate __Cloudwatch Event Logging__
- [x] Investigate __Cloudwatch Event Logging filters__
- [ ] Investigate __Cloudwatch Alerts__
- [ ] Investigate [Alexa Automated Testing](https://github.com/alexa/skill-sample-nodejs-test-automation)
- [ ] Investigate [Alexa Load Testing](https://github.com/alexa/skill-sample-node-js-build-scale-test)
- [ ] Investigate [Alexa Testing](https://github.com/BrianMacIntosh/alexa-skill-test-framework) [looks pretty spiffy]
- [ ] Investigate [Alexa Timeouts](https://github.com/nickclaw/alexa-ability-timeout)
- [ ] Investigate [Virtual Alexa](https://github.com/bespoken/virtual-alexa) [also looks pretty spiffy]
- [x] Investigate Google’s Assistant
