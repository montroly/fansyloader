## Configuration

fansyloader creates a folder `config` at the first start. 
In this folder you can find the configuration file `config.toml` and the log file `fansyloader.log`. 
The configuration file can be opened and edited with any text editor.

### Multiple configurations

Fansyloader can also be started with a different configuration folder. 
To do this, the `-c` flag can be used to specify another configuration order, which will be created if it does not already exist. 

```bash
# example
./fansyloader -c account-1-config
./fansyloader -c account-2-config
```

### Path

The path variable can be used to set the folders in which the files are stored.

* `{{.Provider.Key}}` onlyfans
* `{{.Provider.Name}}` OnlyFans
* `{{.Provider.Domain}}` onlyfans.com
* `{{.Model.Name}}` Name of the Model
* `{{.Model.Username}}` Username of the Model
* `{{.ApiType}}` Through which api the data was loaded. (Example: `posts`, or `messages`)
* `{{.Download.Id}}` The ID of the download. Useful because it can be used to create a unique file name.
* `{{.Download.Ext}}` File extension of the file to be saved (Example: `.png`, `.mp4`)
* `{{.Download.CreateTime}}` Time at which the download was uploaded to the provider.
  * Can be formatted with `{{.Download.CreateTime.Format "2006-01-02_15:04:05"}}`. [Here](https://yourbasic.org/golang/format-parse-string-time-date-example/) you can find an overview of the possible formats.
* `{{.Download.Type}}` video, gif, photo, etc.
* `{{.Download.MimeType}}` The MimeType of the download (Example: `text/plain`)
* `{{.Download.GroupId}}` Id of the object from where the download was obtained. For example, for post video downloads, it would be the id of the post.

In addition, the path can be adjusted via functions. Functions change the output of variables. Available functions are:

* Most [functions from sprig](http://masterminds.github.io/sprig/)
* `cleanFilename` = Attempts to adapt a text so that it can be used as a file or folder name.
  * `꧁༺✿ ᵈᵉᵛⁱˡ᭄𝒈𝒊𝒓𝒍࿐✿༻꧂ / Камыр` becomes `꧁༺✿ ᵈᵉᵛⁱˡ᭄𝒈𝒊𝒓𝒍࿐✿༻꧂-Камы`
* `slug` = Converts the text to a slug
  * `꧁༺✿ ᵈᵉᵛⁱˡ᭄𝒈𝒊𝒓𝒍࿐✿༻꧂ / Камыр` becomes `l-kamyr`
* `toAscii` = Tries to convert the text to an ASCII string
  * `꧁༺✿ ᵈᵉᵛⁱˡ᭄𝒈𝒊𝒓𝒍࿐✿༻꧂ / Камыр` becomes `[-] l[-]]-Kamyr`

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
