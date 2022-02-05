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

### Step 2 ###

Now that we have our base project setup with 3d we need to upgrade the scene to use HDRP. This will require importing a few packages and upgrading our ground material to an HDRP shader.

you can read more about this on unity docs https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@12.1/manual/VR-Overview.html

Basic summary is that we can use any feature or setting within HDRP however we should configure it as we have to optimize for our xr device. It is also important to note that DX12 features are
currently not supported, so we need to make sure we are using DX11 to develop our APK with.

you can find more information about this upgrade process here https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@12.1/manual/Upgrading-To-HDRP.html

The High Definition Render Pipeline (HDRP) uses a new set of Shaders and lighting units, both of which are incompatible with the Built-in Renderer. To upgrade a Unity Project to HDRP, you must first convert all of your Materials and Shaders, then adjust individual Light settings accordingly.

Open our package manager

![Figure 03](Documents/Images/03.png)

now navigate to the unity registry packages from the drop down in the top left corner. from the list select `High Definition RP` and click install. Be patient this can take a few minutes depending on the speed of your machine.

![Figure 04](Documents/Images/04.png)

you can close the package manager now. After installing HDRP the wizard for this should be visible. if it isn't you can access it via `window -> rendering -> HDRP Wizard` 

![Figure 05](Documents/Images/05.png)

the wizard should look like this

![Figure 06](Documents/Images/06.png)

as you can see we have a bunch of errors so click on the `fix all` button at the top under the tabs.. This should help us clear some of these issues up.

![Figure 07](Documents/Images/07.png)

The wizard is going ask if you want to create a default profile, click `create one` to generate it. Again this might take a few minutes depending on your machine, so be patient it will finish.

![Figure 08](Documents/Images/08.png)

Now the wizard should have a bunch of green checks showing that all of the errors have been fixed.

![Figure 09](Documents/Images/09.png)

As you can see our ground plane is now magenta to show that the shader is using the legacy built in material. we need to upgrade our project materials to use HDRP. If you see some errors or warnings in the console ignore them as long as the wizard is green checks then everything is okay.

![Figure 10](Documents/Images/10.png)

### Step 3 ###

Next we are going to click the `convert all built-in materials to hdrp button` the top one

![Figure 11](Documents/Images/11.png)

its going to ask you if you made a backup, ignore and just click `Proceed`. we live on the edge. thats why your here? :) For good measure after you convert i usually click on `upgrade HDRP materials to Latest Version` to double check nothing has errrored.

![Figure 12](Documents/Images/12.png)

now click on the `HDRP + VR` tab in the wizard. you should also see all green checks. You will see a couple warning that the oculus drive needs ot be manually installed.. we performed this within the `unity-xr-project-3d` walk through guide found that we cloned the project from. yay.

![Figure 13](Documents/Images/13.png)

you can also toggle off the show at shart up check box on the bottom of the wizard. now close the wizard

As you can see our grabbable cube is magenta, because it is using the default material. The easiest way to fix this is to make a new material from the `M_Ground` material by copying pasting it within the project tab

![Figure 14](Documents/Images/14.png)

![Figure 15](Documents/Images/15.png)

lets name our new material `M_Cube`. Remember that the prefix `M_` is used on all of our materials so that we can easier search for them with `M_*`

![Figure 16](Documents/Images/16.png)

click on the new material you just renamed in the project tab to view it in your inspector tab. now click on the base map setting to open the color picker. lets make it a different color.

![Figure 17](Documents/Images/17.png)

![Figure 18](Documents/Images/18.png)

now click and drag the green material onto our magenta cube in the scene view.

now we should see our green cube, or whatever else you pick for its color.

![Figure 19](Documents/Images/19.png)

now lets save our scene before we forget. if you see a bunhc of shader errors in the console, just clear them out. As long as you see no magenta on our simple scene everything is ok. very easy for human.

Its important to note that you can access the material upgrade actions within the edit menu -> rendering -> material 

![Figure 20](Documents/Images/20.png)

I also recommend toggling the lights off on your scene view to get unity to generate the shaders for these automagically. once done you can toggle them off. the lighting button is the third one.. you can mouse over for a tooltip.

![Figure 21](Documents/Images/21.png)

### Step 4 ###

when play testing you will notice that our laser pointers are missing, but we can still pick stuff up. lets fix this after we setup some basic lighting. For this we are going to use Global Illumination.

On the bottom right of the unity editor you will see four icons. click on the second to last one, which will bring up your lighting window. you can also access it via the `window -> rendering -> lighting`

![Figure 22](Documents/Images/22.png)

![Figure 23](Documents/Images/23.png)

The lighting window has all of its setting grayed out. click the `new lighting settings` button on the top of the window.

![Figure 24](Documents/Images/24.png)

Its a good idea to make a new directory in your assets folder call `lighting`. lets put our new lighting setting in it.. also name it `Lighting_GI`.

![Figure 25](Documents/Images/25.png)

we are going to toggle on the Real time lighting and turn off baked lighting. we can choose to bake a scene's lighting after we design it. its considered a performance feature, and is not required for local development, as anyone who has baked lighting know its takes a long time, and can eat up alot of storage space. 

![Figure 26](Documents/Images/26.png)

Now we need to tell our Directional light to use real time lighting. not mixed. click on the directional light in your hierachy tab, and in the inspector select realtime from the mode drop down

![Figure 27](Documents/Images/27.png)

next we are going to disable shadows on the ground plane

![Figure 28](Documents/Images/28.png)

also while we are here, lets turn on global illumination and blend probes, this will allow light to bounce off the ground to create more realism.

![Figure 29](Documents/Images/29.png)

configure the cube as well with the same settings

![Figure 30](Documents/Images/30.png)

the last part of this step is to add a few light probes in to the scene. We do this by creating a light probe group, and then adding new probes into white in probe edit mode

![Figure 31](Documents/Images/31.png)

click `edit probes` to move them around in an even fashion, its okay to have some a little below or at floor level to simulate the sun light bouncing off the ground.

![Figure 32](Documents/Images/32.png)

![Figure 33](Documents/Images/33.png)

we should also add a reflection probe in too.

![Figure 34](Documents/Images/34.png)

change the reflection probe type to sphere. for performance we will leave them on baked, also set the size to 8 or so. The maps should auto generate. NOTE: you can toggle off auto generate in your lighting settings if your doing alot of design changes.

![Figure 35](Documents/Images/35.png)

If you play the game you will now notice that your laser pointers are back, our setting configurations tooke care of this automagics. how nice.

![Figure 36](Documents/Images/36.png)