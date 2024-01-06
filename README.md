# Setup Selective for CircleCI

Selective is an intelligent test runner that balances work across nodes, but doesn't stop there. Get real-time test results, intelligent ordering, flake detection, and more.

For more info visit https://selective.ci

Orb installation instructions: https://circleci.com/developer/orbs/orb/selectiveci/setup-selective

## Basic Usage

```yaml
version: 2.1
  orbs:
    setup-selective: selectiveci/setup-selective@0.1.1
  jobs:
    test:
      docker:
        - image: cimg/ruby:3.2
      steps:
        - checkout
        - setup-selective/init:
            run_id: << pipeline.id >>
            actor: << pipeline.trigger_parameters.github_app.user_username >>
            target_branch: main
        - run: bundle install
        - run: bundle exec selective rspec
  workflows:
    test:
      jobs:
        - test
```
