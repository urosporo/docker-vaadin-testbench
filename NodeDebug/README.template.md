# Vaadin Testbench Grid Node - ##BROWSER## Debug

_This image is only intended for development purposes!_ Runs a Selenium Grid Node with a VNC Server to allow you to visually see the browser being automated. Since it runs additional services to support this it is too heavy weight for usage within a Selenium Grid cluster.

## Dockerfile

[`urosporo/testbench-##BASE##-debug` Dockerfile](https://github.com/urosporo/docker-vaadin-testbench/blob/master/##FOLDER##/Dockerfile)

## How to use this image

First, you will need a Vaadin Testbench Grid Hub that the Node will connect to.

```
$ docker run -d -p 4444:4444 --name testbench-hub urosporo/testbench-hub
```

Once the hub is up and running will want to launch nodes that can run tests.

```
$ docker run -d -p 5900:5900 --link testbench-hub:hub -v /dev/shm:/dev/shm urosporo/##BASE##-debug
```

You can acquire the port that the VNC server is exposed to by running:
(Assuming that we mapped the ports like this: 49338:5900)
``` bash
$ docker port <container-name|container-id> 5900
#=> 0.0.0.0:49338
```

In case you have [RealVNC](https://www.realvnc.com/) binary `vnc` in your path, you can always take a look, view only to avoid messing around your tests with an unintended mouse click or keyboard interrupt:
``` bash
$ ./bin/vncview 127.0.0.1:49338
```

If you are running Boot2Docker on Mac then you already have a [VNC client](http://www.davidtheexpert.com/post.php?id=5) built-in. You can connect by entering `vnc://<boot2docker-ip>:49160` in Safari or [Alfred](http://www.alfredapp.com/)

When you are prompted for the password it is __secret__. If you wish to change this then you should either change it in the `/NodeBase/Dockerfile` and build the images yourself, or you can define a docker image that derives from the posted ones which reconfigures it:

``` dockerfile
FROM urosporo/##BASE##-debug:5.1.2

RUN x11vnc -storepasswd <your-password-here> /home/seluser/.vnc/passwd
```

## What is Vaadin Testbench?
_Vaadin Testbench is based on Selenium and automates browsers to test Vaadin-based applications._ That's it! What you do with that power is entirely up to you. Primarily, it is for automating web applications for testing purposes, but is certainly not limited to just that. Boring web-based administration tasks can (and should!) also be automated as well.

Selenium (Vaadin Testbench) has the support of some of the largest browser vendors who have taken (or are taking) steps to make Selenium a native part of their browser. It is also the core technology in countless other browser automation tools, APIs and frameworks.

See the Vaadin Testbench [site](https://vaadin.com/docs/v8/testbench/testbench-overview.html) for documation on usage within your test code.

## License

View [license information](https://github.com/urosporo/docker-vaadin-testbench/blob/master/LICENSE.md) for the software contained in this image.

## Getting Help

### User Group

The first place where people ask for help about Selenium is the [Official User Group](https://groups.google.com/forum/#!forum/selenium-users). Here, you'll find that most of the time, someone already found the problem you are facing right now, and usually reached the solution for which you are looking.

_Note: Please make sure to search the group before asking for something. Your question likely won't get answered if it was previously answered in another discussion!_

### Issues

If you have any problems with or questions about this image, please contact us through a [Github issue](https://github.com/urosporo/docker-vaadin-testbench/issues). If you have any problems with or questions about Vaadin Testbench, please contact Vaadin through Vaadin's [Bug Tracker](https://github.com/vaadin/testbench/issues). If you have any problems with or questions about Selenium, please contact Selenium through Selenium's [Bug Tracker](https://github.com/SeleniumHQ/selenium/issues).

## Contributing

There are many ways to [contribute](http://docs.seleniumhq.org/about/getting-involved.jsp) whether by answering user questions, additional docs, or pull request we look forward to hearing from you.

If you do supply a patch we will need you to [sign the CLA](https://spreadsheets.google.com/spreadsheet/viewform?hl=en_US&formkey=dFFjXzBzM1VwekFlOWFWMjFFRjJMRFE6MQ#gid=0). We are part of [SFC](http://www.sfconservancy.org/)
