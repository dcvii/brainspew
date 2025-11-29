---
title: "IVR: Screening & Recording with PHP and Laravel"
source: "https://www.twilio.com/en-us/blog/developers/tutorials/product/ivr-screening-recording-php-laravel"
author:
  - "[[Mario Celi]]"
published: 2017-01-09
created: 2025-11-19
description: "Create a seamless customer service experience by building an IVR to screen and accept a call or record a voicemail for a live agent at your company with PHP, Laravel, and Twilio."
tags:
  - "clippings"
---
January 10, 2017



---

![ivr-screening-recording-php-laravel](https://www.twilio.com/content/dam/twilio-com/global/en/blog/legacy/2017/ivr-screening-recording-php-laravel/ivr-screening-recording-php-laravel.png "ivr-screening-recording-php-laravel")

This [Laravel](http://laravel.com/) sample application is modeled after a typical call center experience, but with more [Reese's Pieces](https://en.wikipedia.org/wiki/Reese%27s_Pieces#ET:_The_Extra-).

Stranded aliens can call an agent and receive instructions on how to get off of Earth safely. In this tutorial, we'll show you the key bits of code that allow an agent to send a caller to voicemail, and later read transcripts and listen to voicemails.

To run this sample app yourself, [download the code and follow the instructions on GitHub](https://github.com/TwilioDevEd/ivr-recording-laravel).

![IVR Screening and Recording in PHP and Laravel](https://www.twilio.com/content/dam/twilio-com/global/en/blog/legacy/2017/ivr-screening-recording-php-laravel/logo-et-phone2.png)

*See more IVR application builds on [our IVR application page](https://www.twilio.com/docs/voice/interactive-voice-response/).*

## Route the call to an agent

When our alien caller chooses a planet, we need to figure out where to route the call. Depending on their input we will route this call to an extension. Extensions are used to look up an *agent.* Any string can be used to define an extension.

Once we look up the agent, we can use the [<Dial> verb](https://www.twilio.com/docs/voice/twiml/dial) to dial the agent's phone number and try to connect the call.

Editor: this is a migrated tutorial. Find the original code at `https://github.com/TwilioDevEd/ivr-recording-laravel/`

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Database\Eloquent\ModelNotFoundException;
use App\Http\Requests;
use App\Http\Controllers\Controller;
use App\Agent;
use Twilio\Twiml;

class ExtensionController extends Controller
{
    /**
     * Responds with a <Dial> to the caller's planet
     *
     * @return \Illuminate\Http\Response
     */
    public function showExtensionConnection(Request $request)
    {
        $selectedOption = $request->input('Digits');

        try {
            $agent = $this->_getAgentForDigit($selectedOption);
        }
        catch (ModelNotFoundException $e){
            return redirect()->route('main-menu-redirect');
        }

        $numberToDial = $agent->phone_number;

        $response = new Twiml();
        $response->say(
            "You'll be connected shortly to your planet. " .
            $this->_thankYouMessage,
            ['voice' => 'Polly.Amy', 'language' => 'en-GB']
        );

        $dialCommand = $response->dial(
            ['action' => route('agent-voicemail', ['agent' => $agent->id], false),
             'method' => 'POST']
        );
        $dialCommand->number(
            $numberToDial,
            ['url' => route('screen-call', [], false)]
        );

        return $response;
    }

    private function _getAgentForDigit($digit)
    {
        $planetExtensions = [
            '2' => 'Brodo',
            '3' => 'Dagobah',
            '4' => 'Oober'
        ];
        $planetExtensionExists = isset($planetExtensions[$digit]);

        if ($planetExtensionExists) {
            $agent = Agent::where(
                'extension', '=', $planetExtensions[$digit]
            )->firstOrFail();

            return $agent;
        } else {
            throw new ModelNotFoundException;
        }
    }
}
```

With this information, we present our aliens with a list of available agents so they can pick one. Let's see how to look up an agent.

## Look up an agent

When we receive a call from an alien we give them a set of options. In this case the options are:

- For Brodo, press 2
- For Dagobah, press 3
- For Oober, press 4

When our alien caller has made their choice we use the key-press to lookup an `Agent.`

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Database\Eloquent\ModelNotFoundException;
use App\Http\Requests;
use App\Http\Controllers\Controller;
use App\Agent;
use Twilio\Twiml;

class ExtensionController extends Controller
{
    /**
     * Responds with a <Dial> to the caller's planet
     *
     * @return \Illuminate\Http\Response
     */
    public function showExtensionConnection(Request $request)
    {
        $selectedOption = $request->input('Digits');

        try {
            $agent = $this->_getAgentForDigit($selectedOption);
        }
        catch (ModelNotFoundException $e){
            return redirect()->route('main-menu-redirect');
        }

        $numberToDial = $agent->phone_number;

        $response = new Twiml();
        $response->say(
            "You'll be connected shortly to your planet. " .
            $this->_thankYouMessage,
            ['voice' => 'Polly.Amy', 'language' => 'en-GB']
        );

        $dialCommand = $response->dial(
            ['action' => route('agent-voicemail', ['agent' => $agent->id], false),
             'method' => 'POST']
        );
        $dialCommand->number(
            $numberToDial,
            ['url' => route('screen-call', [], false)]
        );

        return $response;
    }

    private function _getAgentForDigit($digit)
    {
        $planetExtensions = [
            '2' => 'Brodo',
            '3' => 'Dagobah',
            '4' => 'Oober'
        ];
        $planetExtensionExists = isset($planetExtensions[$digit]);

        if ($planetExtensionExists) {
            $agent = Agent::where(
                'extension', '=', $planetExtensions[$digit]
            )->firstOrFail();

            return $agent;
        } else {
            throw new ModelNotFoundException;
        }
    }
}
```

Now that our user has chosen their agent, our next step is to connect the call to that agent.

## Call the agent

This code begins the process of transferring the call to our agent.

By passing a `url` to the [`<Number>` noun](https://www.twilio.com/docs/api/twiml/number), we are telling Twilio to make a POST request to the `Agent/Call` route **after** the agent has picked up but **before** connecting the two parties.

Essentially, we are telling Twilio to execute some TwiML that only the agent will hear.

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Database\Eloquent\ModelNotFoundException;
use App\Http\Requests;
use App\Http\Controllers\Controller;
use App\Agent;
use Twilio\Twiml;

class ExtensionController extends Controller
{
    /**
     * Responds with a <Dial> to the caller's planet
     *
     * @return \Illuminate\Http\Response
     */
    public function showExtensionConnection(Request $request)
    {
        $selectedOption = $request->input('Digits');

        try {
            $agent = $this->_getAgentForDigit($selectedOption);
        }
        catch (ModelNotFoundException $e){
            return redirect()->route('main-menu-redirect');
        }

        $numberToDial = $agent->phone_number;

        $response = new Twiml();
        $response->say(
            "You'll be connected shortly to your planet. " .
            $this->_thankYouMessage,
            ['voice' => 'Polly.Amy', 'language' => 'en-GB']
        );

        $dialCommand = $response->dial(
            ['action' => route('agent-voicemail', ['agent' => $agent->id], false),
             'method' => 'POST']
        );
        $dialCommand->number(
            $numberToDial,
            ['url' => route('screen-call', [], false)]
        );

        return $response;
    }

    private function _getAgentForDigit($digit)
    {
        $planetExtensions = [
            '2' => 'Brodo',
            '3' => 'Dagobah',
            '4' => 'Oober'
        ];
        $planetExtensionExists = isset($planetExtensions[$digit]);

        if ($planetExtensionExists) {
            $agent = Agent::where(
                'extension', '=', $planetExtensions[$digit]
            )->firstOrFail();

            return $agent;
        } else {
            throw new ModelNotFoundException;
        }
    }
}
```

Our agent can now be called, but how does our agent interact with this feature? Let's dig into what is happening in the agent's screening call.

## The agent screens the call

When our agent picks up the phone, we use a `[<Gather>](https://www.twilio.com/docs/voice/twiml/gather)` verb to ask them if they want to accept the call.

If the agent responds by entering any digit, the response will be processed by our `connect-message` route. This will `<Say>` a quick message and continue with the original `<Dial>` command to connect the two parties.

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Http\Requests;
use App\Http\Controllers\Controller;
use Twilio\Twiml;

class AgentCallController extends Controller
{
    /**
     * Handles the callback after a call has finished
     *
     * @return \Illuminate\Http\Response
     */
    public function agentVoicemail(Request $request, $agentId)
    {
        $response = new Twiml();
        $callStatus = $request->input('DialCallStatus');

        if ($callStatus !== 'completed') {
            $response->say(
                'It appears that no agent is available. ' .
                'Please leave a message after the beep',
                ['voice' => 'Polly.Amy', 'language' => 'en-GB']
            );

            $response->record(
                ['maxLength' => '20',
                 'method' => 'GET',
                 'action' => route('hangup', [], false),
                 'transcribeCallback' => route(
                     'store-recording', ['agent' => $agentId], false
                 )
                ]
            );

            $response->say(
                'No recording received. Goodbye',
                ['voice' => 'Polly.Amy', 'language' => 'en-GB']
            );
            $response->hangup();

            return $response;
        }

        return "Ok";
    }

    /**
     * Replies with a hangup
     *
     * @return \Illuminate\Http\Response
     */
    public function showHangup()
    {
        $response = new Twiml();
        $response->say(
            'Thanks for your message. Goodbye',
            ['voice' => 'Polly.Amy', 'language' => 'en-GB']
        );
        $response->hangup();

        return $response;
    }

    /**
     * Handles the callback from screening a call
     *
     * @return \Illuminate\Http\Response
     */
    public function screenCall(Request $request)
    {
        $customerPhoneNumber = $request->input('From');
        $spelledPhoneNumber = join(',', str_split($customerPhoneNumber));

        $response = new Twiml();
        $gather = $response->gather(
            ['numDigits' => 1,
             'action' => route('connect-message', [], false),
             'method' => 'GET'
            ]
        );
        $gather->say('You have an incoming call from: ');
        $gather->say($spelledPhoneNumber);
        $gather->say('Press any key to accept');

        $response->say('Sorry. Did not get your response');
        $response->hangup();

        return $response;
    }

    /**
     * Says message during connection between agent and customer (ET)
     *
     * @return \Illuminate\Http\Response
     */
    public function showConnectMessage(Request $request)
    {
        $response = new Twiml();
        $response->say('Connecting you to the extraterrestrial in distress');

        return $response;
    }
}
```

Now our agent can interact with the call, but what if our agent is currently out? In these cases it's helpful to have voicemail set up.

## Send the caller to voicemail

When Twilio makes a request to our voicemail controller, it will pass a [`DialCallStatus`](https://www.twilio.com/docs/api/twiml/dial#attributes-action-dial-call-status-values) which will tell us if the call was successful. If it was "completed" we hang up. Otherwise, we need to `<Say>` a quick prompt and then [`<Record>`](https://www.twilio.com/docs/api/twiml/record) a voicemail from the caller.

We also specify an `[action](https://www.twilio.com/docs/voice/twiml/record/)` for `<Record>`. This route will be called after the call and recording have finished. The route will say "Goodbye" and then `[<Hangup>](https://www.twilio.com/docs/voice/twiml/hangup)`.

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Http\Requests;
use App\Http\Controllers\Controller;
use Twilio\Twiml;

class AgentCallController extends Controller
{
    /**
     * Handles the callback after a call has finished
     *
     * @return \Illuminate\Http\Response
     */
    public function agentVoicemail(Request $request, $agentId)
    {
        $response = new Twiml();
        $callStatus = $request->input('DialCallStatus');

        if ($callStatus !== 'completed') {
            $response->say(
                'It appears that no agent is available. ' .
                'Please leave a message after the beep',
                ['voice' => 'Polly.Amy', 'language' => 'en-GB']
            );

            $response->record(
                ['maxLength' => '20',
                 'method' => 'GET',
                 'action' => route('hangup', [], false),
                 'transcribeCallback' => route(
                     'store-recording', ['agent' => $agentId], false
                 )
                ]
            );

            $response->say(
                'No recording received. Goodbye',
                ['voice' => 'Polly.Amy', 'language' => 'en-GB']
            );
            $response->hangup();

            return $response;
        }

        return "Ok";
    }

    /**
     * Replies with a hangup
     *
     * @return \Illuminate\Http\Response
     */
    public function showHangup()
    {
        $response = new Twiml();
        $response->say(
            'Thanks for your message. Goodbye',
            ['voice' => 'Polly.Amy', 'language' => 'en-GB']
        );
        $response->hangup();

        return $response;
    }

    /**
     * Handles the callback from screening a call
     *
     * @return \Illuminate\Http\Response
     */
    public function screenCall(Request $request)
    {
        $customerPhoneNumber = $request->input('From');
        $spelledPhoneNumber = join(',', str_split($customerPhoneNumber));

        $response = new Twiml();
        $gather = $response->gather(
            ['numDigits' => 1,
             'action' => route('connect-message', [], false),
             'method' => 'GET'
            ]
        );
        $gather->say('You have an incoming call from: ');
        $gather->say($spelledPhoneNumber);
        $gather->say('Press any key to accept');

        $response->say('Sorry. Did not get your response');
        $response->hangup();

        return $response;
    }

    /**
     * Says message during connection between agent and customer (ET)
     *
     * @return \Illuminate\Http\Response
     */
    public function showConnectMessage(Request $request)
    {
        $response = new Twiml();
        $response->say('Connecting you to the extraterrestrial in distress');

        return $response;
    }
}
```

Now let's take a step back to see how to actually record the call.

## Record the caller

When we tell Twilio to record, we have a few [options](https://www.twilio.com/docs/voice/twiml/record#attributes) we can pass to the `<Record>` verb.

Here we instruct `<Record>` to stop the recording at 20 seconds, to [`transcribe`](https://www.twilio.com/docs/api/twiml/record#attributes-transcribe) the call, and to send the transcription to the agent when it's complete.

Notice we redirect to a URL that is specific to this agent. This is a convenient way to specify which agent was called to produce the voice message. This way we can also save the associated agent together with the voicemail.

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Http\Requests;
use App\Http\Controllers\Controller;
use Twilio\Twiml;

class AgentCallController extends Controller
{
    /**
     * Handles the callback after a call has finished
     *
     * @return \Illuminate\Http\Response
     */
    public function agentVoicemail(Request $request, $agentId)
    {
        $response = new Twiml();
        $callStatus = $request->input('DialCallStatus');

        if ($callStatus !== 'completed') {
            $response->say(
                'It appears that no agent is available. ' .
                'Please leave a message after the beep',
                ['voice' => 'Polly.Amy', 'language' => 'en-GB']
            );

            $response->record(
                ['maxLength' => '20',
                 'method' => 'GET',
                 'action' => route('hangup', [], false),
                 'transcribeCallback' => route(
                     'store-recording', ['agent' => $agentId], false
                 )
                ]
            );

            $response->say(
                'No recording received. Goodbye',
                ['voice' => 'Polly.Amy', 'language' => 'en-GB']
            );
            $response->hangup();

            return $response;
        }

        return "Ok";
    }

    /**
     * Replies with a hangup
     *
     * @return \Illuminate\Http\Response
     */
    public function showHangup()
    {
        $response = new Twiml();
        $response->say(
            'Thanks for your message. Goodbye',
            ['voice' => 'Polly.Amy', 'language' => 'en-GB']
        );
        $response->hangup();

        return $response;
    }

    /**
     * Handles the callback from screening a call
     *
     * @return \Illuminate\Http\Response
     */
    public function screenCall(Request $request)
    {
        $customerPhoneNumber = $request->input('From');
        $spelledPhoneNumber = join(',', str_split($customerPhoneNumber));

        $response = new Twiml();
        $gather = $response->gather(
            ['numDigits' => 1,
             'action' => route('connect-message', [], false),
             'method' => 'GET'
            ]
        );
        $gather->say('You have an incoming call from: ');
        $gather->say($spelledPhoneNumber);
        $gather->say('Press any key to accept');

        $response->say('Sorry. Did not get your response');
        $response->hangup();

        return $response;
    }

    /**
     * Says message during connection between agent and customer (ET)
     *
     * @return \Illuminate\Http\Response
     */
    public function showConnectMessage(Request $request)
    {
        $response = new Twiml();
        $response->say('Connecting you to the extraterrestrial in distress');

        return $response;
    }
}
```

#### Legal implications of call recording

If you choose to record voice or video calls, you need to comply with certain laws and regulations, including those regarding obtaining consent to record (such as California’s Invasion of Privacy Act and similar laws in other jurisdictions). Additional information on the legal implications of call recording can be found [in the "Legal Considerations with Recording Voice and Video Communications" Help Center article](https://support.twilio.com/hc/en-us/articles/360011522553-Legal-Considerations-with-Recording-Voice-and-Video-Communications).

*Notice*: Twilio recommends that you consult with your legal counsel to make sure that you are complying with all applicable laws in connection with communications you record or store using Twilio.

Finally, we will see how to view an agent's voicemail.

## View an agent's voicemail

Once we look up the agent, all we need to do is display their recordings. We bind the agent, along with their recordings, to a `View`.

It is possible to look up recordings via the Twilio REST API, but since we have all of the data we need in the `[transcribeCallback](https://github.com/TwilioDevEd/ivr-recording-laravel/blob/33c722f2bddee543940cf5d0c2173cbb0950243b/app/Http/Controllers/AgentCallController.php#L33-L34)` request, we can easily store it ourselves and save a roundtrip.

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Http\Requests;
use App\Http\Controllers\Controller;
use App\Recording;
use App\Agent;

class RecordingController extends Controller
{

    /**
     * Shows an index of existings recordings
     *
     * @return \Illuminate\Http\Response
     */
    public function indexByAgent(Request $request)
    {
        $agentNumber = $request->input('agentNumber');
        $agentNumberInE164Format = '+' . $agentNumber;

        $agent = Agent::where(['phone_number' => $agentNumberInE164Format])
               ->firstOrFail();
        $allRecordings = Recording::where(['agent_id' => $agent->id])->get();

        return response()->view(
            'recordings.index',
            ['recordings' => $allRecordings,
             'agent' => $agent]
        );
    }

    /**
     * Store a new recording from callback
     *
     * @return \Illuminate\Http\Response
     */
    public function storeRecording(Request $request, $agentId)
    {
        $newRecording = new Recording(
            ['caller_number' => $request->input('Caller'),
             'transcription' => $request->input('TranscriptionText'),
             'recording_url' => $request->input('RecordingUrl'),
             'agent_id'      => $agentId]
        );

        $newRecording->save();

        return "Recording saved";
    }
}
```

That's it! We've just implemented an IVR with real Agents, call screening and voicemail.

## Where to next?

If you're a PHP developer working with Twilio, you might want to check out these other tutorials.

**[Part 1 of this Tutorial: ET Phone Home Service - IVR Phone Trees](https://www.twilio.com/docs/voice/tutorials/build-interactive-voice-response-ivr-phone-tree/php/)**

Increase your rate of response by automating the workflows that are key to your business.

**[Appointment Reminders](https://www.twilio.com/docs/messaging/tutorials/appointment-reminders/php/)**

Send your customers a text message when they have an upcoming appointment - this tutorial shows you how to do it from a background job.

#### Did this help?

Thanks for checking out this tutorial! If you have any feedback to share with us, we'd love to hear it. Connect with us [on Twitter](https://twitter.com/twilio) and let us know what you build![From APIs to SDKs to sample apps](https://www.twilio.com/docs)

[

API reference documentation, SDKs, helper libraries, quickstarts, and tutorials for your language and platform.

](https://www.twilio.com/docs)[

The latest ebooks, industry reports, and webinars

Learn from customer engagement experts to improve your own communication.

](https://www.twilio.com/en-us/resource-center)[

Twilio's developer community hub

Best practices, code samples, and inspiration to build communications and digital engagement experiences.

](https://www.twilio.com/en-us/developers)