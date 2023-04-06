---
layout: post
title:  "Git configuration for Windows & WSL"
date:   2023-04-06 13:03:56 +0200
categories: git
---
When cloned projects is used on IDE in Windows (e.g. VS Code, IntelliJ, etc.), but you're using WSL there are some differences in how OSes treat the files:
- difference in system default end-of-line characters 
- difference in filesystem, e.g. not supporting executable bit of a file


## EOL

If you work a lot with Linux like do a lot of scripting, running shell commands, etc. it is worth to switch to Linux defaults, i.e.
- change default EOL in your IDE to LF
- change git `core.eol` to LF (more information in [git docs][core-eol])

{% highlight ini %}
[core]
    eol=lf
{% endhighlight %}

To change it from a command line run:

{% highlight bash %}
git config core.eol lf
{% endhighlight %}

to change the setting on the project level, or run:


{% highlight bash %}
git config --global core.eol lf
{% endhighlight %}

to change the setting on the global level.

## File attributes

Windows filesystem does not support executable bit of a file. Thus, if project files are kept on Windows filesystem, the `core.filemode` setting should be set to `false`. More information about the setting is available in [git docs][core-filemode].

{% highlight ini %}
[core]
    filemode=false
{% endhighlight %}

This will make git ignore the attribute and git will not display attribute changes due to this fact.

To change it from a command line run:

{% highlight bash %}
git config core.filemode false
{% endhighlight %}

to change the setting on the project level, or run:


{% highlight bash %}
git config --global core.filemode false
{% endhighlight %}

to change the setting on the global level.

[core-eol]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-coreeol "core.eol"
[core-filemode]: https://git-scm.com/docs/git-config#Documentation/git-config.txt-corefileMode "core.filemode"
