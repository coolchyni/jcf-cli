# Jedi Code Formatter CLI

I took [Jedi Code Formatter](http://jedicodeformat.sourceforge.net/) (JCF) from [Lazarus IDE repository](https://github.com/graemeg/lazarus/tree/upstream/components/jcf2) and made it as CLI (command line interface) version by removing all the GUI (graphical user interface) parts from the original GUI version. The CLI version can be used as Pascal code formatter in [Visual Studio Code](https://code.visualstudio.com/), or as backend engine of an online [Pascal code beautifier](https://pak.lebah.web.id/jcf).

## How To Build Using Lazarus

1. You must have [Lazarus IDE](http://lazarus-ide.org) already installed on your system.
2. Clone or download this `jcf-cli` GitHub repo into your own folder.
3. Start your Lazarus IDE and open `jcf.lpi` project within `jcf-cli/CommandLine/Lazarus` folder.
4. Build it via Lazarus' **Run** → **Build** menu.
5. Wait while Lazarus is building the JCF project.
6. Take the executable `JCF` file from `jcf-cli/Output/Lazarus` folder along with the `JCFSettings.cfg` configuration file.
7. Just to make sure, test it from Terminal using `./JCF -?` command. It should show the usage manual.

## How To Build Using VS Code

1. You must have both [Free Pascal](http://freepascal.org) compiler and [VS Code](https://code.visualstudio.com) already installed on your system.
2. Clone or download this `jcf-cli` GitHub repo into your own folder.
3. Start your VS Code and open `jcf.lpr` project within `jcf-cli/CommandLine/Lazarus` folder.
4. Build it via VS Code's **Tasks** → **Run Task...** → **JCF: Build Release** menu.
5. Wait while FPC is building the JCF project.
6. Open `test.pas` file from `jcf-cli` folder.
7. Test `JCF` program using **Tasks** → **Run Task...** → **JCF: Test CLI Program** menu and you should see the result in the `test.pas` file.

> **Note:** I've included the executable file for Linux, Mac, and Windows in [`Output/Lazarus`](Output/Lazarus) folder so you don't need to build it yourself. However, it's **not** guaranteed using the latest modification. 😊

## How To Use JCF in VS Code

1. Copy the `JCF` **and** `jcf.xml` config files into your Pascal workspace folder.
2. Create a new VS Code task or open the `tasks.json` if you already have one.
3. Copy the task example below and paste it into your `tasks.json` file.  

  ```json
  {
    "label"  : "JCF: Beautify Code",
    "type"   : "shell",
    "command": "./JCF",
    "args": [
      "${file}",
      "-clarify",
      "-inplace",
      "-config=JCFSettings.cfg"
    ],
    "presentation": {
      "reveal": "never"
    },
    "problemMatcher": []
  },
```
4. It's a task to beautify Pascal code.
5. If you need a task to obfuscate code, simply make another task using the code above, but then change `-clarify` arg into `-obfuscate`.
6. Save your `tasks.json`. Now you should have new JCF's tasks in your tasks list.

## The Problem With JCF

Although JCF is a good Pascal code formatter, it has one single problem that quite annoying. JCF requires the code must be compilable which means it has to be a complete program and syntactically correct. JCF will fail on code snippets or wrong code. To make it works on code snippet, it must be put between a `begin..end` pair and has a correct `program` header, like this:

```pascal
program test;

begin
  // put code snippet here
end.
```

## Demo

Here's JCF CLI in action within VS Code (with [OmniPascal](http://www.omnipascal.com/)):

![](jcf_vscode.gif)

> **Note:** If you're also interested in my other tasks shown in the demo, see my gist about it [here](https://gist.github.com/pakLebah/dab98067e9a388a3a8d2f5c0b44a7d3f).

Hope it's gonna be useful to other Pascal fellows out there. Have fun! 😊

## Changes
The normal version from [git-bee/jcf-cli](https://github.com/git-bee/jcf-cli) is not compatible with the official version of [Jedi Code Formatter](http://jedicodeformat.sourceforge.net/).  So I changed it back to compatible with the official version.

Now you can use this execution with [Pascal Formatter](https://marketplace.visualstudio.com/items?itemName=alefragnani.pascal-formatter) to format pascal code in vscode.