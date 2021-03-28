# JHS Viking Robotics LabVIEW Setup Guide

This guide will walk you through setting up an FRC LabVIEW development environment on your computer. This environment will use LabVIEW FRC, CTRE Phoenix libraries, Sourcetree and Git for Windows, and LabVIEW's source control tools (Professional edition only).

There are several steps, but they are all very simple and rely primarily on program defaults so that you don't need to change anything. This guide is intended for JHS Viking Robotics Team 7221, but will also work for anyone that is interested! Please note that LabVIEW for FRC is only supported on Windows 10, and as such so is this guide.

## Install LabVIEW

First off, you will need to have LabVIEW for FRC set up on your Windows PC. You should contact your FRC Mentors for more information on installation and licensing. To install LabVIEW:

1. Install [LabVIEW 2020 32-bit](https://www.ni.com/en-us/support/downloads/software-products/download.labview-software-for-frc.html) & [Game Tools 2021](https://www.ni.com/en-us/support/downloads/drivers/download.frc-game-tools.html) on your computer. Check [NI's website](https://www.ni.com/en-us.html) for instructions, or search Google for 'Install LabVIEW for FRC'.

2. Configure LabVIEW to seperately store compiled binaries and source code. Open LabVIEW, click ```Tools > Options```, then choose ```Environment```. Check the option for ```Separate compiled code from new files```.

3. Install CTR Electronics [CTRE Phoenix Framework](http://www.ctr-electronics.com/hro.html#product_tabs_technical_resources) on your computer (scroll down to Tech Resources/Installer, and click the most recent .zip file) You can find the downloads, detailed instructions, and controller firmware on their website.

On Windows 10, LabVIEW automatically creates a folder ```C:\Users\Your Username\Documents\LavView Data``` in which several LabVIEW and FRC dependencies are stored. By default, all projects you create will be kept here, which is not very user friendly nor organized. To avoid issues down the line, make a folder ```C:\Users\Your Username\Documents\LabView Code``` in which you will store all of your LabVIEW projects in.

You should now have LabVIEW 2021 for FRC and the CTRE Phoenix Framework installed on your computer. Make sure that when you open the LabVIEW program, you see "LabVIEW FRC 2021" at the top. If not, uninstall LabVIEW and follow step 1 again.

## Install Git and Sourcetree

Now that LabVIEW is set up, you need to set up Git. But first, make sure you have a [GitHub account](https://github.com), and access to your [team's organization](https://github.com/JHS-Viking-Robotics). Once you are sure you have access:

1. Install [Git](https://gitforwindows.org/) to your computer. The defaults are good, but there is one thing to change. When prompted for a default branch name, please select the option that says "main". The default name was "master" for a long time, but as an effort to increase diversity and be more inclusive, we will join the coding community in deprecating this insensitive term. Read more [here](https://github.com/github/renaming/) or through the link in the installer.

2. Install [Sourcetree](https://www.sourcetreeapp.com/) to your computer. Skip the prompt to sign up for Bitbucket. On the next screen, make sure that Sourcetree finds Git on your computer, and then uncheck the box for Mercurial. Next, enter your name and the email account associated with your GitHub account.

Git and Sourcetree should now be installed, and Sourcetree should be set up to use the system Git not embedded Git.

## Configure Sourcetree to use LabVIEW Source Control Tools

LabVIEW professional development environment comes with source control tools which are called as scripts from the command line. LabVIEW FRC ships with the professional environment and will work, but it is important to note that other versions of LabVIEW will not allow you to use the source control tools.

The tools are called as scripts from the command line, and they expect all file paths as absolute file paths. However, Sourcetree and Git both supply relative paths. You need to set up a wrapper script which you use as your source control tool, and that wrapper will expand the relative file paths for LabVIEW.

Long story short, do the following:

1. Make sure that WSL Ubuntu is installed on your computer. You should be able to install it from the [Windows Store](https://www.microsoft.com/store/productId/9N6SVWS3RX71), otherwise check out the [official documentation](https://docs.microsoft.com/en-us/windows/wsl/install-win10).

2. Copy ```_LVCompareWrapper.sh``` to ```C:\Program Files (x86)\National Instruments\Shared\LabVIEW Compare\_LVCompareWrapper.sh```

3. Copy ```_LVMergeWrapper.sh``` to ```C:\Program Files (x86)\National Instruments\Shared\LabVIEW Merge\_LVMergeWrapper.sh```

4. Open Sourcetree and select ```Tools >> Options``` and select ```Diff >> External Diff / Merge```. For ```External Diff Tool```, select ```Custom``` and select the ```_LVCompareWrapper.sh``` file that you just copied, and under ```Arguements``` enter ```\"$REMOTE\" \"$LOCAL\"```.

5. Do the same thing for ```Merge Tool```. Choose the ```_LVMergeWrapper.sh``` file that you copied, and for ```Arguements``` enter ```\"$BASE\" \"$REMOTE\" \"$LOCAL\" \"$MERGED\"```.

At this point you should have Git installed on your computer and Sourcetree should be configured to use it. You should also have LabVIEW FRC 2021 and CTRE Phoenix Framework installed, and LabVIEW should be configured to save all compiled code seperately from your project files. Your machine is ready to go, but you should read on to learn how Git works and how to use it on a team.

## How To Use Source Control With A Team

GitHub provides incredible tools for storing and organizing files, tracking changes, creating branches for seperate projects, and keeping track of development history. However, as Uncle Ben once said in Spider-Man (2002), "With great power comes great responsibility".

It is super important that you talk with your development team, and really anyone who will touch your code, to make sure that everyone knows what conventions and practices to follow. Working together, following strict rules, and using comments everywhere can turn a mind boggling process into a really useful, easy to use one, and help you to avoid "merge hell" and other painful issues.

Check out National Instruments' [GitHub turotial](https://ispring-cloud-45.ispringcloud.com/acc/kc75hpYxMDM3NA/s/10374-oK1iJ-upDjE-L5A0z) for an overview of how Git works, and how programmers can use it to collaborate. There is also a link to a GitHub page with another tutorial that may be useful. If you have used Git before you should still check it out though, as it will help explain some of the quirks of LabVIEW when it comes to Git.

As anything, Google is your friend. National Instruments has lots of documentation but it is not well organized or updated. However, all of the other programs here are industry standard, and you can find infinite tutorials and guides on how to use them. Keep in mind that while many Git tutorials online will show how to use a command line interface with Git, while this may be intimidating the overall process of ```pull >> branch >> program >> commit >> merge >> push``` is the same no matter the interface.

## Help! Nothing Is Working and I'm Confused

Go back and make sure that you did not miss a step. If that doesn't work, try the following:

1. Make sure that LabVIEW has all of its components installed and licensed. Check out [WpLib's FRC Documentation](https://docs.wpilib.org/en/latest/docs/zero-to-robot/step-2/labview-setup.html) if LabVIEW isn't working, and check out [CTRE's Phoenix Documentation](https://docs.ctre-phoenix.com/en/stable/ch05_PrepWorkstation.html) if you have trouble with the Phoenix Framework.

2. Make sure that Git and Sourcetree are working. Check out [Sourcetree Support](https://support.atlassian.com/sourcetree/). Git is not likely to have issues, but Sourcetree may be having issues finding it.

3. You can also check out [this](https://delacor.com/configuring-hg-or-git-to-use-labview-compare-and-labview-merge/) guide for integrating Git and LabVIEW, and [this](https://endigit.com/2017/11/using-labviews-diff-tool-sourcetree) guide which fixes the problems that Sourcetree has when talking to LabVIEW's source control tools.
