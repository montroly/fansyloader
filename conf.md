## Configuration

fansyloader creates a folder `config` at the first start. 
In this folder you can find the configuration file `config.toml` and the log file `fansyloader.log`. 
The configuration file can be opened and edited with any text editor.

### Authentication methods

To download the files, the tool must be associated with a user. 
The program also has to log in to onlyfans with your account. 
A direct login with your username and password is currently not possible, but other methods exist.

fansyloader supports three different methods with their own advantages and disadvantages. 
The methods are briefly explained here and can be set in the configuration under `Auth.source`.

- [Sideloading (Default)](#sideloading--default-)
- [Proxy (Advanced)](#proxy--advanced-)
- [Manual](#manual)

#### Sideloading (Default)

This method is set as default and is the easiest to use.
Here fansyloader tries to find out where your browser stores the files for authentication (cookies). 
When it finds the files, it tries to read and use it.

The disadvantage is that only a few browsers are supported and sometimes several attempts are required for authentication.

* Supported browsers
    * Firefox (tested on **Windows and Linux**)
    * Chrome (tested on **Windows and Linux**)
* Supported OS
    * Windows (tested)
    * Linux (tested)
    * MacOS

**The best experience so far has been with Firefox.**
In case of problems it may be possible that fansyloader has to be started as administrator. (see log)

#### Proxy (Advanced)

This method is the most stable but also the most complicated.
Here fansyloader is set up as a proxy and acts like a MITM attack. 
This is not a risk for you, because you are running the proxy attack yourself.
The advantage is that all browsers are supported and fansyloader acts like your own browser.

How to set up?
* Open the configuration file and set `Auth.source` to `proxy`
* At the first start the file `ca.pem` is created in the `config` folder.
  * You need to add the file to your list of trusted CAs. 
  * If you don't know how to do this, look for instructions on the Internet. 
  * For example [here for Firefox](https://docs.vmware.com/en/VMware-Adapter-for-SAP-Landscape-Management/2.0.1/Installation-and-Administration-Guide-for-VLA-Administrators/GUID-0CED691F-79D3-43A4-B90D-CD97650C13A0.html).
* After that, you need to set up your browser to use the proxy.
  * If you don't know how to do that, search online.
  * For example [here for Firefox](https://www.howtogeek.com/293213/how-to-configure-a-proxy-server-in-firefox/)
  * The proxy is an HTTP proxy and must also be enabled for HTTPS.
  * You must set the address `127.0.0.1` and port `8080` (Via configuration adjustable)
* Go to onlyfans.com

#### Manual

This method works similar to the [onlyfans scraper](https://github.com/DIGITALCRIMINAL/OnlyFans). 
Just store the headers in the configuration under `[Auth.ManualAuth.Headers]` and 
set `Auth.source` to `manual`.