# Keyri Bouncer

## How To Use

```javascript

// import the library
  import { Bouncer } from "keyri-bouncer";
// instantiate the library to load into shadow-dom
  const bouncer = new Bouncer();

// function to process everything
  const processData = async () => {

    // get form data
    const form = document.getElementById("mainForm");

    // data collection / storage
    const data = {};

    // iterate over the els
    Array.from(form.elements).forEach((element) => {
      data[element.id] = element.value;
    });

    // make the call!
    let info = await bouncer.interrogate(
        data.eventType,
        data.userId,
        data.yourPublicKey
    );

    // do something with your data
    console.log({info});

```

## What It Returns

This object represents the response from a user behavior tracking system. Here's a breakdown of its properties:

- `state`: Represents the result of the event. This value is based on your configuration. Possible values are "warn", "allow", "block".

- `ipAddress`: The IP address of the client.

- `userId`: The ID of the user, usually their email address. It's important to validate this value.

- `deviceId`: The unique ID we've assigned to the client's device.

- `wagId`: A looser ID based on the client's machine and IP address.

- `signals`: An array that lists signals detected during the session. These signals will show up in your logs. For example, "max_events_per_timeframe".

- `trustScore`: A score between 0 and 1, calculated based on browser metrics, behavioral analytics, and Bayesian machine learning. The higher the score, the more likely the client is a "good" user.

- `changes`: An array of changes being made to the user or the device. For example, when a new country is added, or a new IP is registered, these changes will be recorded here.

- `event_type`: The type of event logged, like "login", "signup", etc.

- `deviceAge`: The age of the device ID in hours. Since misbehaving device IDs can be blocked, older device IDs are generally better.

Example:

```javascript
{
  "state": "warn",
  "ipAddress": "97.99.80.243",
  "userId": "evil@evil.com",
  "deviceId": "399c6617-6b9b-4c45-a9fb-6b827cf845c5",
  "wagId": "BxZQPgacdjFm6lKADc3F72Pb5o0=",
  "signals": [
    "max_events_per_timeframe"
  ],
  "trustScore": 0.8750399185765636,
  "changes": [],
  "event_type": "login",
  "deviceAge": 18.0242025
}
```