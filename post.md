# Installing Java on a Mac using Jevn

Created: Aug 27, 2020 10:19 AM
Status: Draft

I think its fair to say that going through the process of installing Java on any machine is in of itself a bit confusing. For those that come from NodeJS, installing a new version of Node is as easy as installing `nvm` and running `nvm install [some nodejs version]` and calling it a day.

The goal of this post is to show that we could do just that with Java, install a package to allow us to toggle between Java versions and set our `JAVA_HOME` path automatically for us just by running a few simple commands.

Before we start, ensure that you have `homebrew` installed and that you have updated all dependencies (ie. run `brew upgrade`)

1. First, we need to install `JEnv` using homebrew, run the following command:

    ```bash
    $ brew install jenv
    ```

2. Next, ensure that jenv is listed as a command on your shell, if you are using `bash`, then run

    ```bash
    $ echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.bash_profile
    $ echo 'eval "$(jenv init -)"' >> ~/.bash_profile
    ```

    If using `.zshrc`, then run the following

    ```bash
    $ echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
    $ echo 'eval "$(jenv init -)"' >> ~/.zshrc
    ```

    **Note:** It's important that now you restart your `bash` terminal or run `. ~/.zshrc` to reload your `.zshrc` now that we have added a new command shortcut.

3. Now let's go ahead and download a `brew cask` for the jdk version that we are after. Before we go and download the version that we need, ensure that you run the following command to add the brew repo to your machine ([https://github.com/AdoptOpenJDK/homebrew-openjdk](https://github.com/AdoptOpenJDK/homebrew-openjdk)). Note that to install `oracle-jdk` , check out the instructions listed here [https://formulae.brew.sh/cask/oracle-jdk](https://formulae.brew.sh/cask/oracle-jdk). Note that the following steps will be only to install the AdoptOpenJDK and not the Oracle JDK. If you need some info on the differences between each type, check out [https://www.openlogic.com/blog/java-experts-openjdk-vs-oracle-jdk#:~:text=The biggest difference in OpenJDK,JDK requires a commercial license.&text=Since January 2019%2C businesses now,order to receive software updates](https://www.openlogic.com/blog/java-experts-openjdk-vs-oracle-jdk#:~:text=The%20biggest%20difference%20in%20OpenJDK,JDK%20requires%20a%20commercial%20license.&text=Since%20January%202019%2C%20businesses%20now,order%20to%20receive%20software%20updates).

    ```bash
    $ brew tap AdoptOpenJDK/openjdk
    ```

4. Now that we have the `AdoptOpenJDK`, let's run the following command to install Java 8 (jdk `1.8.x` )

    ```bash
     $ brew cask install adoptopenjdk8
    ```

5. Once the installation completes, we'll then follow up with `jenv` to add this version into our list of available version to be able to toggle between versions. Let's ensure that we know the location where the jdk package was installed, for MacOS Catalina, that should be under the following directory `/Library/Java/JavaVirtualMachines`
6. If we cd into `/Library/Java/JavaVirtualMachines` we should see the following:

    ```bash
    adoptopenjdk-8.jdk
    ```

7. If the above is correct, we'll go ahead and run the following command to add the location of this version to `jenv`

    ```bash
    $ jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home
    ```

8. To confirm that the version is now available on `jenv`, run the following command `jenv versions`, you should see the following output:

    ```bash
    openjdk64-1.8.0.252
    ```

9. Now to add Java 8 as your overall `global` java version, run the following command:

    ```bash
    jenv global openjdk64-1.8.0.252
    ```

10. Now, run `java -version` and you should see the following output:

    ```bash
    openjdk version "1.8.0_252"
    OpenJDK Runtime Environment (AdoptOpenJDK)(build 1.8.0_252-b09)
    OpenJDK 64-Bit Server VM (AdoptOpenJDK)(build 25.252-b09, mixed mode)
    ```

    **Note:** If you still see your old version or nothing at all, ensure that you restart your bash terminal (or .zsrh) to pull in the new path to your Java home (this is set by jenv itself, you don't need to do anything).

That's it! Hopefully it was painless and straightforward, next time you need to toggle between versions, just run `jenv {version}` and you're all set.

You could also set versions of Java specific to your shell terminal, or directory, simply replace `global` with `local` (if you are within a specific directory) or `shell` for adding a version to specific to the shell you're running.
## Resources:
* [https://www.jenv.be/](https://www.jenv.be/)
* [https://github.com/jenv/jenv](https://github.com/jenv/jenv)
* [https://installvirtual.com/install-openjdk-8-on-mac-using-brew-adoptopenjdk/](https://installvirtual.com/install-openjdk-8-on-mac-using-brew-adoptopenjdk/)
* [https://www.openlogic.com/blog/java-experts-openjdk-vs-oracle-jdk#:~:text=The biggest difference in OpenJDK,JDK requires a commercial license.&text=Since January 2019%2C businesses now,order to receive software updates](https://www.openlogic.com/blog/java-experts-openjdk-vs-oracle-jdk#:~:text=The%20biggest%20difference%20in%20OpenJDK,JDK%20requires%20a%20commercial%20license.&text=Since%20January%202019%2C%20businesses%20now,order%20to%20receive%20software%20updates)