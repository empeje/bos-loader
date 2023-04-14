# BOS Component Loader

Serves a local directory of component files as a JSON payload properly formatted to be plugged into a BOS `redirectMap`. When paired with a viewer configured to call out to this loader, it enables local component development—especially when working on multiple components in parallel.

Works best when paired with [FroVolod/near-social](https://github.com/FroVolod/near-social) for component syncing and CI/CD

## Requirements

Currently, you must run a viewer instance yourself locally. See [Local Component Development](https://github.com/near/near-discovery#local-component-development)

## Installation

see GitHub Releases

## Usage

```sh
Usage: bos-loader [OPTIONS] <ACCOUNT_ID>

Arguments:
  <ACCOUNT_ID>

Options:
  -p, --path <PATH>  [default: .]
  -h, --help         Print help
  -V, --version      Print version
```

The only required argument is the account which you want to serve the components from

e.g. running from a directory with `HelloWorld.jsx` in the following way

```bash
bos-loader michaelpeter.near
```

results in

```json
{
  "components": {
    "michaelpeter.near/widget/HelloWorld": {
      "code": "return <>Hello World</>;"
    }
  }
}
```

## Multi-device Testing

Run both your viewer and loader behind [ngrok](https://ngrok.com/) to test on multiple devices or share your working copy with others!

Example ngrok config:

```yml
authtoken: <automatically populated during setup>
tunnels:
  web:
    proto: http
    addr: 127.0.0.1:3000
    subdomain: my-viewer # change this
  api:
    proto: http
    addr: 127.0.0.1:3030
    subdomain: my-loader # change this and use in your viewer config
version: "2"
region: us
```

Then start with `ngrok start --all`
