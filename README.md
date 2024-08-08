# oily-ci

A ci which doesn't depend on 3 abstractions, yaml, some meta-yaml-language and a git forge.

It's a POC showcase of [hay](https://www.oilshell.org/release/0.22.0/doc/hay.html).

## Usage

- install [oils](https://www.oilshell.org/release/0.22.0/). At least Version 22.
- run `./oily-ci.ysh gear.hay`
- Take a look at gear.hay which is how a CI file would look like.


TODOS to make this actually usable
- make it composable. Inheritance, of tasks, etc.
- make if configurable (e.g. not depend on podman)
- Security and stuff
- make it "interactable". e.g. outputs like Artifacts, listen to webhooks, download a repo, etc.
