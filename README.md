
# Tableau Python Server - Beta
[![Community Supported](https://img.shields.io/badge/Support%20Level-Community%20Supported-457387.svg)](https://www.tableau.com/support-levels-it-and-developer-tools)

Tableau Python Server (TabPy) is part of Tableau's expanding range of extensibility options. These include [R execution](http://onlinehelp.tableau.com/current/pro/desktop/en-us/help.html#r_connection_manage.html) via the calculation editor interface, along with the web data connector SDK, the JavaScript API, the REST API, the Tableau Data Extract API, and Tableau Document API. For details, see the [Tableau Developer Portal](https://community.tableau.com/community/developers).

For all questions not related to the TabPy code (installation, deployment, connections, Python issues, etc.) and requests use [Server & Online Administration Forum](https://community.tableau.com/community/forums/server-administration) on [Tableau Community](https://community.tableau.com).

TabPy framework allows Tableau to remotely execute Python code. It has two components:

1. A [server](server.md) process built on Tornado, which allows for the remote execution of Python code through a set of REST APIs. Code can either be immediately executed or persisted in the server process and exposed as a REST endpoint, to be called later.
2. A [client library](client.md) that enables the deployment of such endpoints, based on Python functions.

Tableau can connect to the TabPy server to execute Python code on the fly and display results in Tableau visualizations. Users can control data and parameters being sent to TabPy by interacting with their Tableau worksheets, dashboard or stories.

You can find detailed **installation instructions** for TabPy server [HERE](server.md).

To run Python code in your Tableau calculated fields, enter the address and port number for a TabPy server instance in Tableau.

<p align="center"><img alt="Screenshot of Configuration on Tableau Desktop" src="external-service-configuration.png"></p>

On Tableau Server, use the [tabadmin](https://onlinehelp.tableau.com/current/server/en-us/tabadmin.htm) command line utility to configure a TabPy connection.


```
tabadmin stop
tabadmin set vizqlserver.extsvc.host <ip address or host name of the machine hosting TabPy>
tabadmin set vizqlserver.extsvc.port <port for TabPy>
tabadmin configure
tabadmin start
```

It is not necessary to install TabPy on the Tableau Server or Desktop computer-all that is required is a pointer to a TabPy server instance.

Once the configuration is done, you can use Python in calculated fields in Tableau. You can learn more about authoring Python calculations in Tableau [HERE](TableauConfiguration.md).


<p align="center"><img alt="Screenshot of a Python calculated field on Tableau Desktop" src="python-calculated-field.png"></p>


## Useful Resources
  - [Building advanced analytics applications with TabPy](https://www.tableau.com/about/blog/2017/1/building-advanced-analytics-applications-tabpy-64916)
  - [TabPy Tutorial on TabWiki](https://community.tableau.com/docs/DOC-10856)
  - [Running TabPy in Docker containers](https://hub.docker.com/r/emhemh/tabpy/)


## Security Considerations
The following security issues should be kept in mind as you use TabPy with Tableau:
  - The data channel between Tableau and TabPy is currently not encrypted.
  - TabPy currently does not use authentication.
  - Python scripts can contain code which can harm security on the server where the TabPy is running. For example:
    - Access file system (read/write)
    - Install new Python packages which can contain binary code
    - Execute operating system commands
    - Open network connections to other servers and download files
