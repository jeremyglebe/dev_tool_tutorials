# Using Cygwin With Your C++ VSCode Dev Environment

## Subject
Once you've already [set up your VSCode environment on Windows](https://github.com/jeremyglebe/dev_tool_tutorials/tree/master/win_vsc) you may find
yourself feeling like MinGW wasn't enough to bridge the Windows-GNU gap. If you
need more GNU features so that you and your Linux/MacOS friends can both run
the same code, you might consider installing Cygwin. Where MinGW just ports a
few GNU tools over to Windows, Cygwin creates an entirely new environment on
your system. In essence, when you compile with Cygwin you aren't considered to
be using Windows. You are considered to be using the Unix-like Cygwin platform.
This is very helpful, but there is a setup process.

## Requirements
The following is assumed about your environment:
* You are familiar with downloading files and navigating windows directories
* You have [followed this tutorial](https://github.com/jeremyglebe/dev_tool_tutorials/tree/master/win_vsc) and have VSCode installed properly on your Windows machine

## Install [Cygwin](https://cygwin.com/install.html)
* Download and run `setup-x86_64.exe`
* Choose `Install from internet`
* Choose whatever path you'd like for Cygwin, just **make sure to remember it**
    * later we will be using the `bin` folder inside the folder you installed to
* The rest of the settings you can leave as default until you reach `Choose a Download Site`, you can pick any of these sites.
    * After the downloads complete, the package selector will launch
* Alongside all the default packages, you need to install
    * `bash-completion`
    * `gcc-core`
    * `gcc-g++`
    * `chere`
* Click the next button until installation completes
    * You should make sure to create a desktop shortcut when it asks

## Using Cygwin Terminal in VSCode
Cygwin has its own built-in terminal, and all your handy GNU features are only
available in that terminal. So how can we get this terminal to be used in
VSCode? We have two methods. I will explain here how to make Cygwin your
default terminal. However, I don't actually recommend that. I will be writing
a separate tutorial on how to use different terminals in VSCode. If you follow
that tutorial, you can avoid making Cygwin your default (which would not be
preferable in all situations) and instead just use it when needed. If you want
to proceed with making it your default terminal, follow the steps below:
* Click `file>preferences>settings` in the top left
* Search for `settings.json` and click `Edit in settings.json`
* Find `terminal.integrated.shell.windows`
    * Change its line to the following (Replacing PATH_TO_CYGWIN with that path that you totally remembered from earlier)
    `"terminal.integrated.shell.windows": "PATH_TO_CYGWIN\\bin\\bash.exe"`
    * If the line isn't there, create it. **Don't remove the outer {} braces**
* Add these lines below the `terminal.integrated.shell.windows` line
```
"terminal.integrated.env.windows": {
    "CHERE_INVOKING": "1"
},
"terminal.integrated.shellArgs.windows": [
    "--login",
    "-i"
],
```
* Cygwin uses a special root folder instead of the usual Windows "C:\\\\"
    * We will tell our terminal to use this folder
* Add the following line to `settings.json`, careful **not to remove the outer {} braces**,
`"code-runner.terminalRoot": "/cygdrive/"`

## Open Cygwin in a folder?
Do you want to be able to open your Cygwin terminal in any folder (easily)?
You can set up a right-click menu option to open the terminal. (That menu is
called the "context menu") To add Cygwin's terminal to the context menu, [follow
the advice on this Stack Overflow page.](https://stackoverflow.com/questions/9637601/open-cygwin-at-a-specific-folder) Don't want to follow the link? That's
okay. It is really easy. Here's the important part:
```
After Cygwin is launched, open up a Cygwin terminal (as an administrator)
and type the command:
chere -i -t mintty -s bash.
Now you should have "Bash Prompt Here" in the Windows right-click context menu.
```

## Conclusion
That's it! Cygwin should now work in your existing VSCode environment. Using
`Run Code` should now use Cygwin's build tools.
I really really recommend running Cygwin not as your default terminal, but as
on of many using the Shell Launcher extension. This will cause problems with
Code Runner (CR will only use the default terminal) but these problems will
be addressed in the Shell Launcher tutorial.