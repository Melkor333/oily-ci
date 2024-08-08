# oily-ci

A "CI" which doesn't depend on 3 abstractions, yaml, some meta-yaml-language and a git forge.

It's a POC showcase of [hay](https://www.oilshell.org/release/0.22.0/doc/hay.html).

# what is it?

Everything here is ysh:
- The "ci-engine" (`oily-ci.ysh`)
- The configuration (`gear.hay`)
- The script which is run inside of the container (see [gear.hay](./gear.hay))

But the core idea is that the *configuration* is written in `ysh`/`hay`.

# Usage

- install [oils](https://www.oilshell.org/release/0.22.0/). At least Version 22.
- run `./oily-ci.ysh gear.hay`
- Take a look at [gear.hay](./gear.hay) which is how a CI file would look like.
- TODO: run `./oily-ci.ysh gear.ysh` (currently broken because sourcing hay doesn't work well)
- Take a look at [gear.ysh](./gear.ysh) which is how a CI with custom logic might look
  - TODO: Currently it has no logic. But it could have (almost) all logic oils provides -> almost because the idea is that it's evaled in a sandbox

# Why?

Typically CI uses "yaml + something". and that something gets real bad real quick.
Also, `yaml` is a really [bad configuration language](https://noyaml.com/) without any "builtin" logic.
But sadly people WANT logic in their configuration. And this is where it will always go wrong quick with a simple abstract thing.

Typical CIs with yaml do something along the lines of:
- write yaml with nested shell snippets
- Add in special kinds of variable expansions and the like
- Add special variables IN the yaml to say e.g. "run this job 10 times with slightly different variables"

With `oily-ci` the idea is that you can just write a `.ysh` file to do all of it for you.
This `.ysh`-file is run (at some point hopefully in a sandbox) and generates JSON output.
That json output only contains a very simple structure of variables.
- No more variable expansion
  - TODO: passing variables between jobs is done with env vars. since oils can use json `json write (&myvar)` this isn't as painful as it was in bash
- No more "shell in yaml". "Shell in hay" is first class and therefore simple pain!
- No more special variables for some logic. Because `ysh` provides logic to e.g. create a task 10 times.
- This also means that the "final" json can be generated and inspected locally, without any CI. (of course without magic variables which would be filled out by a CI)

# TODO

TODOS to make this actually usable
- Make it composable. Inheritance, of tasks, etc.
- Make if configurable (e.g. not depend on podman)
- Proper containerization? Right now it's a very cheap "podman" line
- Security and stuff
- Make it "interactable". e.g. outputs like Artifacts, listen to webhooks, download a repo, etc.
- Write the actual engine in Go or so and just "shell out" to ysh for parsing/evaluating the configuration
