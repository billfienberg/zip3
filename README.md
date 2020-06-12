# zip3

## Background

Using the first three digits of a US zip code, you can roughly approximate which metropolitan area that zip code is associated with.

## Demo

![zip3 gif](https://raw.githubusercontent.com/billfienberg/zip3/61fc975d14cf37eb0efe812bcb27028f53b2f706/zip3-demo.gif)

Code Sandbox: https://codesandbox.io/s/zip3-demo-rj8oc

## Data

https://en.wikipedia.org/wiki/List_of_ZIP_Code_prefixes

## High Level Design

This package exports a dictionary where the keys are the three-digit zip code prefixes, and the values are objects containing `id` (the three-digit zip), `city`, and `state` (if available).

For example:

```js
{
  "440": { "id": "440", "city": "Cleveland", "state": "OH" }
}
```

## Usage

```js
import { useState } from "react"
import zips from "zip3"

function MetroParser() {
  const [zip, setZip] = useState("90210")
  const shortenedZip = zip.slice(0, 3)
  const metroObject = zips[shortenedZip] || {}
  const { city, state } = metroObject
  const metroString = city && state ? `${city}, ${state}` : ""

  return (
    <div>
      <label>
        Zip code:
        <input
          type="number"
          placeholder="44114"
          value={zip}
          onChange={(e) => {
            const { value } = e.target
            setZip(value)
          }}
        ></input>
      </label>
      <p>Metro: {metroString}</p>
    </div>
  )
}
```
