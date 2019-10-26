# SMC-Connect SMS

[![Build Status](https://travis-ci.org/smcgov/ohana-sms-smc.png?branch=master)](https://travis-ci.org/smcgov/ohana-sms-smc) [![Code Climate](https://codeclimate.com/github/smcgov/ohana-sms-smc/badges/gpa.svg)](https://codeclimate.com/github/smcgov/ohana-sms-smc) [![Dependency Status](https://gemnasium.com/smcgov/ohana-sms-smc.svg)](https://gemnasium.com/smcgov/ohana-sms-smc) [![Test Coverage](https://codeclimate.com/github/smcgov/ohana-sms-smc/badges/coverage.svg)](https://codeclimate.com/github/smcgov/ohana-sms-smc)

SMC-Connect SMS is San Mateo County's customized version of
[Ohana SMS][ohana-sms], a Ruby on Rails application that allows people in need
who lack access to the internet to find human services via SMS.

[ohana-sms]: https://github.com/monfresh/ohana-sms

You can try the service by sending a 5-digit ZIP code to these numbers:

**English:** 650-227-9909

**Spanish:** 650-802-8934

## Stack Overview

* Ruby version 2.5.7
* Rails version 5.2.0
* Testing Frameworks: MiniTest

## Local Installation

### Prerequisites
You'll need a Ruby development environment on your computer, and a Twilio account.

#### Ruby
If you're on a Mac, the easiest way to get up and running is to run @monfresh's
[laptop script](https://github.com/monfresh/laptop). On Linux, you'll need to
install [Build tools][build-tools], [Ruby with RVM][ruby], and [Node.js][node].

Once your environment is ready to go, install the app:

```
git clone git@github.com:smcgov/ohana-sms-smc.git && cd ohana-sms-smc
bin/setup
```

[build-tools]: https://github.com/codeforamerica/howto/blob/master/Build-Tools.md
[ruby]: https://github.com/codeforamerica/howto/blob/master/Ruby.md
[node]: https://github.com/codeforamerica/howto/blob/master/Node.js.md

#### Twilio
If you're a maintainer of the San Mateo County version of Ohana SMS, you will
need access to San Mateo County's Twilio account. Otherwise, if you're
interested in deploying your own version of Ohana SMS, please refer to the
[Ohana SMS instructions](https://github.com/monfresh/ohana-sms#twilio).

1. Once logged in to your Twilio account, visit the [Account Settings][settings]
page.
2. Copy your AuthToken and paste it in `config/application.yml`
next to `twilio_auth_token`.

[settings]: https://www.twilio.com/console/project/settings

## Deploy to Heroku

SMC-Connect SMS is already deployed to Heroku. If you're a maintainer of
SMC-Connect SMS, please request access to San Mateo County's Heroku account.

## Customizing and translating the SMS messages

Currently, what can be translated are the greetings and instructions.
The search results content, such as the Location names, or the short
descriptions, are not translated.

To modify the existing translations, you can edit them directly on GitHub if
you have write access to this repo. Here are the edit links for the [English]
and [Spanish] text.

[English]: https://github.com/smcgov/ohana-sms-smc/edit/master/config/locales/en.yml
[Spanish]: https://github.com/smcgov/ohana-sms-smc/edit/master/config/locales/es.yml

To translate the messages into a new language, copy and paste the contents of
`config/locales/en.yml` into a new file in `config/locales` with a filename
corresponding to the language's two-character code, and with a `.yml`
extension. Then translate the text from English into your desired language.
See `config/locales/es.yml` as an example. For more details, read the
[Rails Internationalization Guide](http://guides.rubyonrails.org/i18n.html).

Once your translations are in place, [buy a new number][number] in your
Twilio account that will be used for a particular language. Then follow these
instructions:

1. Go to the Twilio [Manage Numbers][manage] page and click on your number.

2. Under `Messaging`, in `Request URL`, enter
`https://ohana-sms-smc.herokuapp.com/locations/reply?locale=[language_code]`,
where `[language_code]` is the 2-letter code for your desired language.
For example, French would be `?locale=fr`.

3. Select `HTTP GET` from the dropdown, and click `Save`.

[number]: https://www.twilio.com/user/account/phone-numbers/search
[manage]: https://www.twilio.com/user/account/phone-numbers/incoming

## Running the tests

Run tests locally with this command:

    script/test

To see the actual tests, browse through the [test] directory.

[test]: https://github.com/monfresh/ohana-sms/tree/master/test

Credits
-------

Created by [Moncef Belyamani](https://twitter.com/monfresh).

Inspired by and built upon the work of
[Mark Silverberg](https://github.com/marks/ohana-sms).

### Public domain

This project is [dedicated to the public domain](LICENSE.md).
As stated in [CONTRIBUTING](CONTRIBUTING.md):

> This project is in the public domain within the United States, and copyright
> and related rights in the work worldwide are waived through the
> [CC0 1.0 Universal public domain dedication][CC0].
>
> All contributions to this project will be released under the CC0 dedication.
> By submitting a pull request, you are agreeing to comply with this waiver of
> copyright interest.

[CC0]: https://creativecommons.org/publicdomain/zero/1.0/
