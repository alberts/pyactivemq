# Maintainer Wanted #

This project is no longer being maintained. I am writing software using [Go](http://golang.org) these days. If anyone wants to take over to complete the update to the latest ActiveMQ-CPP, please contact me.

# News #

pyactivemq 0.1.0 has been released (supporting ActiveMQ-CPP up to version 2.2.6). Check the Featured Downloads.

On Windows, you might need to install one of the following:
  * [Microsoft Visual C++ 2008 SP1 Redistributable Package (x86)](http://www.microsoft.com/downloads/details.aspx?familyid=A5C84275-3B97-4AB7-A40D-3802B2AF5FC2&displaylang=en)
  * [Microsoft Visual C++ 2008 SP1 Redistributable Package (x64)](http://www.microsoft.com/downloads/details.aspx?familyid=BA9257CA-337F-4B40-8C14-157CFDFFEE4E&displaylang=en)

# Introduction #

pyactivemq is a [Python](http://www.python.org/) module for communicating with the [ActiveMQ](http://www.activemq.org/) message broker which implements the [Java Message Service](http://en.wikipedia.org/wiki/Java_Message_Service) specification.

pyactivemq wraps the [ActiveMQ-CPP](http://activemq.apache.org/cms/) library using [Boost.Python](http://www.boost.org/libs/python/doc/). This implies that both the [Stomp](http://stomp.codehaus.org/) and Openwire wire formats are supported for communicating with the broker.

pyactivemq could also be used with other JMS message brokers by utilising ActiveMQ's [JMS to JMS bridge](http://activemq.apache.org/jms-to-jms-bridge.html) feature.

It would also be possible to create a CMS wrapper for the C libraries that are part of Sun's OpenMQ broker (formerly known as Sun Java System Message Queue). pyactivemq could then be extended to support both ActiveMQ and OpenMQ.

# Getting Started #

Refer to the [Building](Building.md) page on the wiki to get started. For some more ideas of what's possible, check the [Examples](Examples.md).