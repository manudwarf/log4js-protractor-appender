# log4js-protractor-appender
Log4js appender suited for Protractor

[![Build Status](https://travis-ci.org/manudwarf/log4js-protractor-appender.svg?branch=master)](https://travis-ci.org/manudwarf/log4js-protractor-appender)


## What is it for?

Log4js is a very powerful tool to provide logs in a NodeJS application and/or test suite. Unfortunately, it poorly integrates with Protractor, as the latter uses a "control flow" system that runs tasks in a very particular order.

`log4js-protractor-appender` ensures logging is integrated with the control flow, and display logging in the proper order.

It also resolves promises passed as arguments before outputting them.

Example:

    logger.info('Navigating to /');
    browser.get('/');
    logger.info('Displayed text is:', element(by.css('#someText')).getText());
    logger.info('Should be displayed last');

Outputs without `log4js-protractor-appender`:

    [INFO] Navigating to /
    [INFO] Should be displayed last
    [INFO] Displayed text is: [Promise object]

Outputs with `log4js-protractor-appender`:

    [INFO] Navigating to /
    [INFO] Displayed text is: Some Text
    [INFO] Should be displayed last


## Setup

`log4js-protractor-appender` overrides log4js' default console appender. Just install it as a dependency:

    npm install log4js-protractor-appender --save

Then you can load it as any console appender. For example:

    {
        "appenders": [
            {
                "type": "log4js-protractor-appender"
            }
        ]
    }
