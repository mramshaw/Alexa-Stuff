# Alexa-Stuff

![Alexa Icon](/Images/alexaLogo2x._V516058141_.png)

As a game developer, I've experimented with TTS (Text to Speech) systems such as
[Festival](http://www.cstr.ed.ac.uk/projects/festival/) to produce game dialogue.
Achieving natural-sounding results is a lot of work. Good voice actors are expensive,
and for good reason. A lot of work is required. TTS systems are not as much work, but
the results are not anywhere near as realistic either (generally placeholder quality
only).

Alexa is impressive. While the regional voices vary in quality, they all sound fairly
natural - with little of the robotic quality often found with TTS systems.

## Bits and bobs of stuff for Alexa development

#### Trivia

There are Easter Eggs in Alexa:

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

#### Alexa Slots

While Alexa has some very useful built-in slots, it's probably a 'best practice' to define
custom slots. For one thing, the built-in slots are extensive and it is probably a good
idea to restrict these quite a bit. Follow the following link for some useful tips on
[formatting slot values](https://developer.amazon.com/docs/custom-skills/define-the-interaction-model-in-json-and-text.html#cert-custom-slot-types).

#### Memory Usage

The smallest possible allocation for a Lambda Function is 128 MB. So it is a good idea to
use this as a target, rather than trying to minimize memory usage with procedural code.

#### Logging

Each invocation (a request or reponse) will generate 2 log events (a START event and an END
event) so the urge to log every interesting user interaction is probably to be avoided.
Even so, for debugging reasons it is important to log every __significant__ event (user
responses, unhandled events, enough life cycle events for context). There is a rich market
for logging analysis, which should be a warning to be careful about what gets logged - for
privacy reasons, if not just to reduce the log clutter.

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
- [ ] Investigate the use of __Account Linking__ and __Permissions__
- [ ] Investigate __Cloudwatch Event Logging__
- [ ] Investigate [Alexa Automated Testing](https://github.com/alexa/skill-sample-nodejs-test-automation)
- [ ] Investigate [Alexa Load Testing](https://github.com/alexa/skill-sample-node-js-build-scale-test)
- [ ] Investigate [Alexa Testing](https://github.com/BrianMacIntosh/alexa-skill-test-framework) [looks pretty spiffy]
- [ ] Investigate [Virtual Alexa](https://github.com/bespoken/virtual-alexa) [also looks pretty spiffy]
- [x] Investigate Google’s Assistant
