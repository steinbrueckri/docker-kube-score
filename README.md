# Kube-score

![Dependabot](https://flat.badgen.net/dependabot/steinbrueckri/docker-kube-score?icon=dependabot)
[![](https://images.microbadger.com/badges/version/steinbrueckri/kube-score.svg)](https://hub.docker.com/r/steinbrueckri/kube-score)

## Why

If you search the official `kube-score` image please go to [zegl/kube-score](https://github.com/zegl/kube-score/)).

The Official Image didn't fit for my usecase so I had to adjust it a bit so I could easily use it in a Google Cloud Build.

## What

`kube-score` is a tool that performs static code analysis of your Kubernetes object definitions.

The output is a list of recommendations of what you can improve to make your application more secure and resilient.

You can test kube-score out in the browser with the [online demo](https://kube-score.com) ([source](https://github.com/kube-score/web)).

## Hows

```yml
steps:

  #############################################################################################################
  # Running kube-ccore
  #############################################################################################################

  - id: kube-score monitoring
    name: 'steinbrueckri/kube-score:latest
    entrypoint: 'bash'
    args:
      - -c
      - |
        shopt -s globstar nullglob && kube-score score --output-format ci --ignore-test "service-type" /workspace/resources/monitoring/**/*.{yaml,yml}  || exit 0
    waitFor: ['-']
```

## Release

- create new branch
- make your changes, if needed
- commit your changes like
  - Patch Release: `fix(script): validate input file to prevent empty files`
  - Minor Release: `feat(dockerimage): add open for multiple input files`
  - Major Release [look her](https://github.com/mathieudutour/github-tag-action/blob/master/README.md)
