# Overview

This a PoC for encapsulating HTTP responses on Cardano chain that can be retrieved via cardano-graphql using custom URI `cardano+metadata://$TX_ID?network=$NETWORK&key=$METADATUM_LABEL&type=http-response`.

`type=http-response` is an optional parameter that allows the library to parse the metadata JSON object as if it were an actual HTTP response and then, return a mocked axios response [(more info here)](https://github.com/repsistance/cardano-meta-handler/blob/main/examples/examples.js#L4). If it's not parsed, the plain JSON object is returned "as it is" on-chain.

It defaults to use [dandelion.link's](https://gimbalabs.com/#/open-source-apis/graphql-api) `cardano-graphql` deployments that can be overriden passing a valid URL via `graphql` query string parameter.

I currently have tested using nodejs, but should build and work on browsers :shrug:

# Build

```
npm install
npm run build
```

# Run by examples

```
# get tx metadata as it is on-chain (gzip+base64)
node examples/get-plain-metadata.js

# aplication/pgp-signature example
node examples/get-http-response-metadata.js | jq . 

# aplication/ld+json example
node examples/get-http-response-metadata2.js | jq .

# verify rcmorano's 3D-ADA json-ld response from Cardano chain
node examples/verify-pgp-metadata.js

# build txmetadata object from file:/// uri
node examples/build-txmeta-from-file.js

# build tx metadata object from https:// uri
node examples/build-txmeta-from-weburl.js
```

Check [examples](examples/examples.js) for some comments. 
