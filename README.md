# serverless-ruby-circleci

A CircleCI orb to build and deploy Serverless Ruby apps.

## Usage

Here's an example to test, build & deploy a Serverless Ruby application.

```yaml
version: 2.1

orbs:
  serverless-ruby: codegram/serverless-ruby@0.0.3

workflows:
  main:
    jobs:
      - serverless-ruby/test
      - serverless-ruby/deploy:
          requires:
            - serverless-ruby/test
          filters:
            branches:
              only: master
```

This orb has some assumptions:

1. Your whole test suite can be executed with `bundle exec rspec`
2. You're using the Serverless framework
3. If you need DynamoDB, it installs it checking the presence of `serverless-dynamodb-local` plugin

Before using it, make sure to:

1. Add your project's AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY to CircleCI project settings.
2. Add `rspec_junit_formatter` to your `Gemfile` test group.

See the [orb page](https://circleci.com/orbs/registry/orb/codegram/serverless-ruby) for more information about its options.

## Development

Validate the orb config with:

```
circleci orb validate orb.yml
```

Then publish a development version (it will expire in 90 days) and test it:

```
circleci orb publish orb.yml codegram/serverless-ruby@dev:0.0.X
```

When you're sure everything works OK you can publish a production version with:

```
circleci orb publish orb.yml codegram/serverless-ruby@0.0.X
```
