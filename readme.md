# Keyri Bouncer

## How To

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
        data.yourAppKey,
        data.eventType,
        data.userId,
        data.yourPublicKey
    );

    // do something with your data
    console.log({info});

```