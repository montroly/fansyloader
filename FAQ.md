# FAQ

#### Where can I find the source code?

Nowhere. The source code is not public.

#### Are you planning to publish the source code?

No.

#### How can I switch between Onlyfans and Fansly?

You can set a default value in `config.toml` under `provider`. 
Alternatively you can call fansyloader with flags

```bash
# For onlyfans
./fansyloader --onlyfans
# For fansly
./fansyloader --fansly
```

#### Why is something new not scrapped?

Fansyloader remembers what it has already downloaded and skips it. 
Thus, it is faster and does not stress the providers' websites so much.
However, if something new has been acquired, it will not be recognized because it will be skipped.
As a solution, there are two options:

1. the crowbar: delete the file `config/db.sqlite`.
2. elegant: 

```bash
# remove skip for all users
fansyloader db unset-skip

# remove skip for one user
fansyloader db unset-skip --username awesome-user
```

#### What do I do if I don't care about the load on the providers webiste?

Set in the configuration `[Download] enable_optimizations = false`

#### Why can I perform a maximum of 20 parallel downloads?

The question is, when was the last time you watched 20 videos in parallel?

#### Can I speed up the download?

Yes, you can increase the `request_limit` value in the configuration or set it to `0` to disable the limit. 
You can also use `max_downloads` to increase the number of simultaneous downloads.

#### How do I verify the GPG signature?

Fansyloader signs all binaries with a [GPG key](https://keys.openpgp.org/search?q=montroly%40protonmail.com) to prevent against unwanted modification of binaries. 
To validate the binary, download the signature file which ends in `.asc` for the binary you downloaded and use the gpg command line tool.

```
gpg --keyserver keys.openpgp.org --recv 6D7B6383B9212F1FA5E073D8D8D2D9BCE14926F5
gpg --verify fansyloader-{{< version >}}.asc fansyloader-{{< version >}}
``` 

Look for the text `Good signature from "montroly <montroly@protonmail.com>"` to assert a good binary,
despite warnings like `This key is not certified with a trusted signature!`.

#### How do I know I can trust the program?

Not at all, as usual. 
But you can check it with a virus scanner or online tool. 
You could monitor the network communication with Wireshark or something else. 

I can tell you that the program does not do anything different from what I have stated here. - It downloads files.

#### Can I download something I can't see? Can I download something I didn't pay for? Can I download messages that I have not received?

No
