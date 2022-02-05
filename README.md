# unity-xr-project-hdrp
Generic Unity 3d XR virtual reality project using HDRP, XRI toolkit, OpenXR, Oculus SDK and input system.

## Overview ##

Step by step instructions on how to build the base 3d HDRP repository / project for simple 3d HDRP XR unity projects.. lazy programmers -> clone one of the releases to access this.

when building Vr projects need to change the xr plugin -> android settings for the specific device we are building for. If not OpenXR builds will display in your oculus home room, there we will need independent builds for oculus and friends. This guide will instruct you. and is based off of this project template https://github.com/BatCountryEntertainment/unity-xr-project-3d

This is easy human, very easy. You will be a meta pro in no time using simple guide.

## BUILDING 3D HDRP VR PROJECT WITH MOST RECENT UNITY SETTINGS : PART 1 - SETUP ##

### Step 1 ###

First create a new project in unity 2021.2.10f1 using the `unity-xr-project-3d` repository found here https://github.com/BatCountryEntertainment/unity-xr-project-3d

go to this repo, and clone it into a new project directory onto your computer

easiest way to do this is to use git hub desktop client, and when your browser prompts to open in desktop client select that and choose a location to download to.

![Figure 01](Documents/Images/01.png)

Alternative you can also download the zip of the project and extract that to an existing repo that you might have setup.

Then load the new project directory you extracted into unity hub, and load the project. select `add project from disk`

After it loads open the sample scene

![Figure 02](Documents/Images/02.png)