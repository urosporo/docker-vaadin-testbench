# Vaadin Testbench Docker Grid Hub

The Hub receives a test to be executed along with information on which browser and 'platform' where the test should be run. The hub will use this information and delegate to a node that can service those needs.

## Dockerfile

[`urosporo/testbench-hub` Dockerfile](https://github.com/urosporo/docker-vaadin-testbench/blob/master/Hub/Dockerfile)

## How to use this image

```
$ docker run -d -p 4444:4444 --name testbench-hub urosporo/testbench-hub
```

Note: You can optionally override default configuration settings using environment variables.
See the [Hub's Dockerfile](Dockerfile) to view the list of variables and their default values.

```
$ docker run -d -p 4444:4444 --name testbench-hub -e GRID_TIMEOUT=10 urosporo/testbench-hub
```


Once the hub is up and running will want to launch nodes that can run tests. You can run as many nodes as you wish.

```
$ docker run -d --link testbench-hub:hub -v /dev/shm:/dev/shm urosporo/testbench-node-chrome
$ docker run -d --link testbench-hub:hub -v /dev/shm:/dev/shm urosporo/testbench-node-firefox
```

## What is Vaadin Testbench?
_Vaadin Testbench is based on Selenium and automates browsers to test Vaadin-based applications._ That's it! What you do with that power is entirely up to you. Primarily, it is for automating web applications for testing purposes, but is certainly not limited to just that. Boring web-based administration tasks can (and should!) also be automated as well.

Selenium (Vaadin Testbench) has the support of some of the largest browser vendors who have taken (or are taking) steps to make Selenium a native part of their browser. It is also the core technology in countless other browser automation tools, APIs and frameworks.

See the Vaadin Testbench [site](https://vaadin.com/docs/v8/testbench/testbench-overview.html) for documation on usage within your test code.

## License

View [license information](https://github.com/urosporo/docker-vaadin-testbench/blob/master/LICENSE.md) for the software contained in this image.

## Getting Help

### Issues

If you have any problems with or questions about this image, please contact us through a [Github issue](https://github.com/urosporo/docker-vaadin-testbench/issues). If you have any problems with or questions about Vaadin Testbench, please contact Vaadin through Vaadin's [Bug Tracker](https://github.com/vaadin/testbench/issues). If you have any problems with or questions about Selenium, please contact Selenium through Selenium's [Bug Tracker](https://github.com/SeleniumHQ/selenium/issues).
