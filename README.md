# Guidelines

This guide reflects our current development practices we have adopted for all of
our open source projects. This is a [Ribose's fork] of the [thoughtbot's guide].
It's mostly similar with some minor adjustments.

If you are contributing to any of our open source projects then it's highly
expected that you follow this guidelines, but if you have some different opinion
about any of the rules then please open [an Issue] for details discussion.

High level guidelines:

* Be consistent.
* Don't rewrite existing code to follow this guide.
* Don't violate a guideline without a good reason.
* A reason is good when you can convince a teammate.

## General

* [Best practices]
* [Git Protocol]
* [Code review]

## Ruby projects

For Ruby based projects we are using [ruby-style-guide], which is based on the
[bbatsov-guide] with some customized preferences. Once you start a new project
then please add this [rubocop-config] to the project and then [configure-hound]
to automated this process in every PR's.

Once everything is setup, [Hound CI] should comment on each of the PR's whenever
there is a violations and please do not merge it until you resolves those.

## Credits

This guide is maintained by [Ribose Inc.]


[Ribose Inc.]: https://www.ribose.com/
[Ribose's fork]: https://github.com/riboseinc/guides
[thoughtbot's guide]: https://github.com/thoughtbot/guides
[an Issue]: https://github.com/riboseinc/oss-ruby-contribution-guide/issues

[Best practices]: https://github.com/thoughtbot/guides/tree/master/best-practices
[Git Protocol]: https://github.com/thoughtbot/guides/tree/master/protocol/git
[Code review]: https://github.com/thoughtbot/guides/tree/master/code-review

[ruby-style-guide]: https://github.com/thoughtbot/guides/tree/master/style/ruby
[bbatsov-guide]: https://github.com/bbatsov/ruby-style-guide
[rubocop-config]: style/.rubocop.yml
[configure-hound]: style/.hound.yml
[Hound CI]: https://houndci.com
