# oily-ci

A "CI" which doesn't depend on 3 abstractions, yaml, some meta-yaml-language and a git forge.

It's a POC showcase of [hay](https://www.oilshell.org/release/0.22.0/doc/hay.html).


Everything here is ysh:
- The "ci-engine" (`oily-ci.ysh`)
- The configuration (`gear.hay`)
- The script which is run inside of the container (see [gear.hay](./gear.hay))

But the core idea is that the *configuration* is written in `ysh`/`hay`.
The reason is that this is typically yaml + something. and that something gets real bad real quick.
Also, `yaml` is a really [bad configuration language](https://noyaml.com/) without any "builtin" logic.
But sadly people WANT logic in their configuration. And this is where it will always go wrong quick with a simple abstract thing.

## Usage

- install [oils](https://www.oilshell.org/release/0.22.0/). At least Version 22.
- run `./oily-ci.ysh gear.hay`
- Take a look at gear.hay which is how a CI file would look like.


TODOS to make this actually usable
- Make it composable. Inheritance, of tasks, etc.
- Make if configurable (e.g. not depend on podman)
- Security and stuff
- Make it "interactable". e.g. outputs like Artifacts, listen to webhooks, download a repo, etc.
- Write the actual engine in Go or so and just "shell out" to ysh for parsing/evaluating the configuration
