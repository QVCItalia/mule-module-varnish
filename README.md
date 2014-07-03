# Mule Varnish Module

Varnish is an HTTP accelerator designed for content-heavy dynamic web sites. In contrast to other HTTP accelerators, such as Squid, which began life as a client-side cache, or Apache and nginx, which are primarily origin servers, Varnish was designed as an HTTP accelerator. Varnish is focused exclusively on HTTP, unlike other proxy servers that often support FTP, SMTP and other network protocols.

This module will allow you to interact with Varnish Administration port and sending instructions like banning and purging cache.

## Installation

The module can either be installed for all applications running within the Mule instance or can be setup to be used
for a single application.

*All Applications*

Download the module from the link above and place the resulting jar file in
/lib/user directory of the Mule installation folder.

*Single Application*

To make the module available only to single application then place it in the
lib directory of the application otherwise if using Maven to compile and deploy
your application the following can be done:

Add the connector's maven repo to your pom.xml:

    <repositories>
        <repository>
            <id>mule-ee-snapshots</id>
            <name>Mule Snapshot Repository</name>
            <url>http://dev.ee.mulesource.com/repository/content/repositories/snapshots/</url>
            <layout>default</layout>
        </repsitory>
    </repositories>

Add the connector as a dependency to your project. This can be done by adding
the following under the dependencies element in the pom.xml file of the
application:

    <dependency>
        <groupId>org.mule.modules</groupId>
        <artifactId>mule-module-varnish</artifactId>
        <version>1.0-SNAPSHOT</version>
    </dependency>

## Usage
**Config: <varnish:config/>**

Parameters

+ name: configuration name
+ host: Varnish machine IP address
+ port: Varnish administrator port, usually 6082
+ secret: secret string, it can be found in /etc/varnish/secret Varnish machine
+ version (optional):  Varnish release used

Example

	<varnish:config name="VarnishConfig" host="10.211.55.115" port="6082" secret="1483dcc6-7643-4d4e-b250-3254e40c1d2f" version="4.4.0" />


**Ban: <varnish:ban-url/>**

Parameters

+ config-ref (optional): reference to a configuration tag
+ url: URL that it has to be banned
+ host (optional): see Config 
+ port (optional): see Config
+ secret (optional): see Config
+ version (optional): see Config

N.B. 
If config-ref is not set, host, port, secret and version must be set. Even if config-ref is set, if one of host, port, secret or version is set, all of the others must be set.

Example

	<varnish:ban-url config-ref="VarnishConfig" url="/api/nodes?path=test" />

