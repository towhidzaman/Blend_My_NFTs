
<p align="center">
  <img src="https://user-images.githubusercontent.com/82110564/145726253-99c5540e-dead-4355-a99f-37afc702862c.png">
</p>

# Blend_My_NFTs

## Description

Blend_My_NFTs is a work-in-progress Blender add-on that can automatically generate thousands of images, animations, or 3D objects to help you launch your NFT colleciton! Blend_My_NFTs is beign created by This Cozy Studio to launch an NFT collection called This Cozy Place. If you would like to learn more about Blend_My_NFTs or This Cozy Place, please visit our discord server: https://discord.gg/UpZt5Un57t 

![NFT_Test_Render_17](https://user-images.githubusercontent.com/82110564/142952463-5764566e-1402-40a4-9cca-a9c57105f033.png)
*Test sample of the NFT collection This Cozy Place rendered in Blender 2.93 using Blend_My_NFTs (prior to commit 223).

## Features 
- Generate and export Images, Animations, and 3D Models at the same time or individually.
- Generate all possible combinations of your NFTs! The only limit is your imagination, and your processing power...
- Raritize and weight your attributes.
- Preview data about your NFT collection; Time to render and the possible combinations.
- Inbuilt metadata template generation for Solana, Cardano, and Ethereum.

There are always new features dropping, join our discord to stay tuned for updates!

## Official Links: 

Website: https://thiscozystudio.com/

Discord: https://discord.gg/UpZt5Un57t 

Twitter: https://twitter.com/CozyPlaceNFT

Instagram: https://www.instagram.com/this_cozy_place/

Youtube: https://www.youtube.com/channel/UCARiKfuoSghM6DeieqWylYQ

Reddit: https://www.reddit.com/r/ThisCozyPlace/

# Blend_My_NFTs Tutorial Guide

Blend_My_NFTs, this readme tutorial material, the youtube tutorials, and the live stream Q/As and tutorials are all provided for free by me for anyone to access/use any way they like. I only ask in return that you credit this software if you use Blend_My_NFTs to launch an NFT collection and kindly share what I have built here. A direct link to the Blend_My_NFTs Github page on your collection website (or equivelant) would sefice. I ask you of this only to share this tool and what it can do as I feel there are many out there that would benefit from it, my only goal is to help those that need it. It brings warmth to my heart that so many people use what I have built. Thank you.

The software in its current state is not farily user friendly but with a really basic understanding of programing you can opporate it easily. You can learn the programing skillz needed in ten minutes! :)

Blend_My_NFTs works with Blender 3.0.0 on Windows 10 or macOS Big Sur 11.6. 

## Youtube Tutorial Series

Link to the Blend_My_NFTs Tuotrial series on Youtube: 
https://www.youtube.com/watch?v=dUajXAZzSPc&list=PLuVvzaanutXetnvsa2_xvXvpREUEYfpg1

Note - Though this video series may be helpful, it is not up to date with the current Blend_My_NFTs release. This document has more detailes and may have newer information. If you have no experience with the Blender API I recomend watch this tutorial on running python scripts in Blender: https://www.youtube.com/watch?v=cyt0O7saU4Q 


## Important Terminology 

Before we can continue there are terms that I will be using to describe the process of this software and make it a bit easier to understand. Refer to this section if you come accross an unfamiliar term. 

For the following terms, lets say you are creating an NFT collection where the image is of a person wearing a hat:

``Attribute`` A part of an NFT that can be changed. The hat on a man is an Attribute, there are many types of hats, but the hat itself I will refer to it as an attribute.

``Variants`` These are the types of hats; red hat, blue hat, green hat, cat hat, etc. These can be swapped into the hat Attribute with one another to create different NFTs. 

``DNA`` DNA is a sequence of numbers that determins what Variant from every Attribute in an NFT collection to include in a single NFT image. This program generates a uniqe DNA sequence for every possible combination of Variants in Attributes. 

``Batch`` A Batch is a randomly selected subset of NFT DNA. It is a smaller portion of the total number of NFTs you want to generate. This makes the work load of rendering thousands of images easier to manage. It also gives you the option to render on multiple computers and ensures each computer renders seperate images with no overlap.

# Installation and Getting Started

This youtube tutorial goes over the basic setup discussed in this section: https://www.youtube.com/watch?v=dUajXAZzSPc (This video is out of date but goes over how to run scripts in Blender which is important to running Blend_My_NFTs)

Follow these steps to setup Blend_My_NFTs:

1. At the top of this page click the green "Code" button
2. Click "Download Zip" - This will download the Blend_My_NFTs folder to your Downloads folder in zip format
3. In your download folder, move Blend_My_NFTs-main.zip to your desktop or another easily accessable location
4. Unzip the file:
- How to unzip a file on Mac: https://support.apple.com/en-ca/guide/mac-help/mchlp2528/mac
- How to unzip a file on Windows: https://support.microsoft.com/en-us/windows/zip-and-unzip-files-f6dde0a7-0fec-8294-e1d3-703ed85e7ebc
5. Move the Blend_My_NFTs-main folder is located on your Desktop for easy access (recomended)
6. Rename the Blend_My_NFTs-main folder to Blend_My_NFTs (optional)

## How to set up your .Blend file 

The following section covers how to set up your .Blend file and config.py file

In order for Blend_My_NFTs to read your .blend file, you need to structure your scene in a specific way. Please follow all naming and collection conventions exactly, otherwise the scripts will not run properly. 

**Important Note**

Your .blend file must be moved to the Blend_My_NFTs folder. When you run the script, the .blend file must be in the directory of the Blend_My_NFTs folder. The Blender text editor has some weird quirks that make finding the right directory a bit tricky. If you are interested, I suggest reading about it in the Blender API above. This is the only work around I could find for now. 

Rules for .blend structure: 

- All Objects, collections, light sources, cameras, or anything else you want to stay constant for each NFT insert it into a collection named "Script_Ignore" exactly. This collection should be located directly beneath the 'Scene Collection' in your .blend file. Every thing in this Script_Ignore collection will be ignored by the collection (Attribute) fetcher. The state of the render and viewport camera of any objects/collections in Script_Ignore will remain unchanged during the scripts operation. The script will not turn the cameras of anything located in Script_Ignore on or off, so however you set them, will be how it renders.

- Every Attribute of your NFT must be represented by a collection directly beneath the 'Scene Collection' in your .blend file. DO NOT USE NUMBERS OR UNDERSCORES IN THE NAME OF THESE COLLECTIONS, this will mess with the scripts. Only use capital letters and lowercase letters, no numbers(0-9) or the underscore symbol( _ ). 

- For each Variant of each Attribute create a collection containing everything that makes up that Variant. This Variant collection must be placed within the Attribute collection and named with the following format: VariantName_(variant number begining at 1)_0 (e.g. Cube_1_0, Cube_2_0, etc.). The VariantName CANNOT CONTAIN NUMBERS OR UNDERSCORES. Like above, this will mess with the scripts.
 
Here is an example of proper scene and collection formating with the above conventions:

<img width="405" alt="Screen Shot 2021-11-22 at 7 24 00 PM" src="https://user-images.githubusercontent.com/82110564/142954386-92372667-72e9-4568-a8f0-aae270f705fb.png">

In this example ``Camera`` ``and Const Collection 1`` is in ``Script_Ignore`` and will be displayed in every NFT generated. The collection ``Cube`` represents an attribute, and the collections ``Cube_1_33``, ``Cube_2_33``, ``Cube_3_33``, and ``Cube_4_1`` are the variants of that attribute. Notice that each variant of Cube has an incrementing number representing the order of the variants. The numbers ``33``, ``33``, ``33``, and ``1`` represent the percentage chance that variant will get chosen if ``enableRarity`` is set to ``True``. 

## Customizing the config.py file

After installation, open the Blend_My_NFTs folder. You will need to change variables in the config.py file with a text editor or IDE; I recomend Visual Studio Code, but Blender has a bilt in Text Editor for ease of use. config.py is where you can customize aspects of your NFT collection and how it is generated.

Description of customisable variables to generate images: 

``nftName`` - A string representing name of the file exported by Blend_My_NFTs (REQUIRED)


``imageFileFormat`` - A string representing the image file format that Blend_My_NFTs will export generated images as: (REQUIRED)

     Type the exact name provided below in the '' for the imageFileFormat:
  
    'JPEG' - Exports the .jpeg format
  
    'PNG' - Exports the .png format
  
    Visit https://docs.blender.org/api/current/bpy.types.Image.html#bpy.types.Image.file_format for a complete list of file formats supported by Blender. Enter the     file extension exactly as specified in the Blender API documentation.

``animationFileFormat`` - A string representing the animations file format that Blend_My_NFTs will export generated animations as: (REQUIRED)

    Type the exact name provided below in the '' above:
    
    AVI_JPEG - Exports the .avi jpeg format
    
    AVI_RAW - Exports the .avi raw format
    
    FFMPEG - Exports the .ffmpeg format
    
    Visit https://docs.blender.org/api/current/bpy.types.Image.html#bpy.types.Image.file_format for a complete list of file formats supported by Blender. (These       are the Blender only supported animation formats).

``modelFileFormat`` - A string representing the 3D Models file format that Blend_My_NFTs will export generated 3D Modles as: (REQUIRED)

    Type the exact name provided below in the '' above:
    
    fbx - The .FBX file format
    
    glb - The .glb file format
    
    obj - The .obj file format *Exports both a .obj and a .mtl files for the same generated object
    
    x3d - The .x3d file format
    
    Visit https://docs.blender.org/api/current/bpy.ops.export_scene.html?highlight=export_scene#module-bpy.ops.export_scene
    for a complete list of object formats supported by Blender.


``save_path_mac`` - A string representing the save path for Blend_My_NFTs if you are on MacOS: (REQUIRED - if on MacOS)

    Example mac: /Users/Path/to/Blend_My_NFTs


``save_path_windows`` - A string representing the save path for Blend_My_NFTs if you are on Windows: (REQUIRED - if on Windows)

    Example windows: C:\Users\Path\to\Blend_My_NFTs


``maxNFTs`` - A positive integer representeing the number of NFTs to generate. (REQUIRED)


``nftsPerBatch`` - A positive integer representing the number of NFTs per batch. (REQUIRED)


``renderBatch`` - A positive integer representing the the batch number to render if ``renderImage`` is set to True. (REQUIRED)


``enableExporter`` - A Boolean value, when set to True, will export Images and or 3D models when main.py is run in Blender. (Turned on after NFTRecord.json and appropriate batches are generated with main.py)

``enableImages`` - A boolean value, when set to True with ``enableExporter = True`` will export images. 

``enableAnimations`` - A boolean value, when set to True with ``enableExporter = True`` will export animations. 

``enableModelsBlender`` - A boolean value, when set to True with ``enableExporter = True`` will export 3D models. 

- Note that ``enableImages`` and ``enableModelsBlender`` can run at the same time. Both images and models will be exported. (One of the above is REQUIRED)


``enableResetViewport`` - A boolean value, when set to True, resets the veiwport of all cameras not in Script_Ignore. (Optional)


``enableGeneration`` - A boolean value, when set to True, applies and takes into account colour or material variants in the NFT DNA. (Optional)


``generationType`` - A string value, takes ``color`` or ``material`` as input. Determines if extra variatns are generated with colours or material textures. (Optional)


``rgbaColorList#`` - A list containing tuples representing the RGBA colour values assigned to a given object in ``colorList``. (Optional)


``materialList#`` - A list containing strings representing the names of materials in blender: (Optional)

    These materials must be in your Current Files' Materials. Make sure that you've set your materials as "fake user". The collections below are Current Files'         Materials. You can put as many or as little materials values in these lists as you would like. You can create any number of materialLists and assign them to       any number of collections that you would like. Each set of materialLists assigned to an object by collection name in the materialList will act like an             attribute and create a unique variant of that item.


``colorList`` - A dictionary which the keys are the names of variants, and the items are the ``rgbaColorList#`` or ``materialList#``: (Optional)

    The rgbaColorList# deterimnes the colours that the variants will change to. This creates new variants with those RGBA colour values. 

## Running main.py - Generating NFTRecord and Batches

Before you can render iamges you need to generate a list of NFT DNA then split it up into batches to render more easily. These will take the form of the NFTRecord.json file, and a list of Batch#.json files. 

``NFTRecord.json`` - This file contains a list of all NFT DNA, this list is limited by ``nftMax`` in config.py. 

``Batch#.json`` - These files contain peices of NFTRecord.json selected at random and sent to a batch containing ``nftsPerBatch`` number of DNA. 

Before running main.py, ensure these variables are set properly or else the script will not work:  

- ``nftName``
- ``save_path_mac`` or ``save_path_windows``
- ``maxNFTs``
- ``nftsPerBatch``
- ``enableExporter = False``

Steps to generate NFTRecord and Batches:

1. In your .blend file open the ``Scripting Tab`` in the menu of Blender: 

<img width="1440" alt="Screen Shot 2021-10-24 at 9 51 25 PM" src="https://user-images.githubusercontent.com/82110564/138623488-9d0efc07-4004-4d3a-a7fe-25cb6050ac51.png">

2. Click the "Open" button in the Blender Text Editor:

<img width="1422" alt="Screen Shot 2021-10-29 at 11 31 38 PM" src="https://user-images.githubusercontent.com/82110564/139518856-7798ea86-0be0-4511-bc87-fa09ce2f6538.png">

3. With the Blender File View open, navigate to the Blend_My_NFTs folder, navigate to the ``src`` folder, then open main.py.

<img width="1062" alt="Screen Shot 2021-11-23 at 8 09 23 PM" src="https://user-images.githubusercontent.com/82110564/143153066-254e5e3e-cd06-4fdb-b645-180ed01fe89b.png">

5. To run main.py click the run button shown circled below:

<img width="605" alt="Screen Shot 2021-11-23 at 8 12 10 PM" src="https://user-images.githubusercontent.com/82110564/143153297-b90d9e16-69b7-4b44-b63b-20869f155f32.png">

If you correctly formated your .blend file, you will now have two files; an NFTRecord.json, and a number of Batch#.json files located in the ``Batch_Json_files`` folder. 

## Running main.py - Generating Images

**For this section, ensure you have generated NFTRecord.json and Batch#.json files before taking the following steps**

Steps to Generate Images: 

1. Ensure all manditory variables have been filed in (all found in config.py): 
- ``nftName``
- ``save_path_mac`` or ``save_path_windows``
- ``maxNFTs``
- ``nftsPerBatch``
- ``renderBatch``

2. Run main.py in Blender with ``enableExporter`` set to ``False`` in config.py. This will generate the NFTRecord.json and Batch#.json files. 

3. Set ``renderBatch`` to the batch number you wish to render in config.py. 

4. Set ``enableExporter`` to ``True`` in config.py. 

5. Set ``enableImages`` to ``True`` in config.py.

6. Run main.py in the Blender Scripting Tab. This will now generate Images.

<img width="605" alt="Screen Shot 2021-11-23 at 8 12 10 PM" src="https://user-images.githubusercontent.com/82110564/143153297-b90d9e16-69b7-4b44-b63b-20869f155f32.png">

## Summery: The order to run main.py to Generate Images

Run the scripts in the following order: 
1. main.py - With ``renderImage`` set to ``False`` in the config.py: Generates the data for your NFT collection.
2. main.py - With ``renderImage`` set to ``True`` in the config.py: Renders images in a batch specified by ``renderBatch``.

## Running main.py - Generating Animations

Steps to Generate Animations: 

1. Ensure all manditory variables have been filed in (all found in config.py): 
- ``nftName``
- ``save_path_mac`` or ``save_path_windows``
- ``maxNFTs``
- ``nftsPerBatch``
- ``renderBatch``

2. Run main.py in Blender with ``enableExporter`` set to ``False``. This will generate the NFTRecord.json and Batch#.json files. 

3. Set ``animationFileFormat`` to the animation file format you wish to export in config.py. 

4. Set ``enableAnimations`` to ``True`` in config.py.

5. Set ``enableExporter`` to ``True`` in config.py.

6. Run main.py in the Blender Scripting Tab. This will now generate Animations.

<img width="605" alt="Screen Shot 2021-11-23 at 8 12 10 PM" src="https://user-images.githubusercontent.com/82110564/143153297-b90d9e16-69b7-4b44-b63b-20869f155f32.png">

## Summery: The order to run main.py to Generate Animations

Run the scripts in the following order: 
1. main.py - With ``enableExporter`` set to ``False`` in config.py: Generates the data for your NFT collection. 
2. main.py - With ``enableExporter`` and ``enableAnimations`` set to ``True`` in config.py: Renders and compiles animations.

## Running main.py - Generating 3D Models from a .blend file

Youtube tutorial for generating 3D models: https://www.youtube.com/watch?v=rRs0lN5huDk&t=1s

Steps to Generate 3D models: 

1. Ensure all manditory variables have been filed in (all found in config.py): 
- ``nftName``
- ``save_path_mac`` or ``save_path_windows``
- ``maxNFTs``
- ``nftsPerBatch``
- ``renderBatch``

2. Run main.py in Blender with ``enableExporter`` set to ``False``. This will generate the NFTRecord.json and Batch#.json files. 

3. Set ``modelFileFormat`` to the 3D Model file format you wish to export in config.py. 

4. Set ``enableModelsBlender`` to ``True`` in config.py.

5. Set ``enableExporter`` to ``True`` in config.py.

6. Run main.py in the Blender Scripting Tab. This will now generate 3D Models.  

<img width="605" alt="Screen Shot 2021-11-23 at 8 12 10 PM" src="https://user-images.githubusercontent.com/82110564/143153297-b90d9e16-69b7-4b44-b63b-20869f155f32.png">

## Summary: The order to run main.py to Generate 3D Models: 

run the scripts in the following order:
1. main.py - With ``enableExporter`` set to ``False`` in config.py: Generates the data for your NFT collection. 
2. main.py - With ``enableExporter`` and ``enableModelsBlender`` set to ``True`` in config.py: Exports 3D models.

# Generating 3D Models with external 3D Models

This youtube tutorial goes over the basic setup discussed in this section: https://www.youtube.com/watch?v=NonORFpVhLw (This video is out of date but may be of use)

The following section covers generating and exporting 3D models with Blend_My_NFTs with a repository of external 3D models in a folder structure. The 3D model generator combines 3D models together and exports all possible combinations of those 3D models to a folder. 

## How to set up your 3D model folders

Similarly to the Image Generator, there is a specific way to format 3d model repositors external to Blender. 

1. In the following photo we have a folder structure. In this example, ``Sphere`` and ``Cube`` are our attributes. Any object file in the ``Script_Ignore_Folder`` will be added to all NFT 3D models generated, and such is an appropriate place to put constant scene elements you wish to appear in every NFT you generate. 

<img width="191" alt="Screen Shot 2021-11-09 at 8 55 34 PM" src="https://user-images.githubusercontent.com/82110564/141035340-576f5ca6-8710-4ce1-a9ad-a28c75653c6e.png">

2. After you have formated the repository of 3D models to the above convention, copy and past it into the 3D_Model_Input folder located in Blend_My_NFTs: 

<img width="357" alt="Screen Shot 2021-11-09 at 8 59 06 PM" src="https://user-images.githubusercontent.com/82110564/141035754-3561ae2b-ee5c-4d65-ac5e-d4c17e34e3a7.png">

3. Next open config.py and change the variable ``use3DModels = False`` to ``use3DModels = True``

<img width="150" alt="Screen Shot 2021-11-09 at 9 02 05 PM" src="https://user-images.githubusercontent.com/82110564/141035910-5ffb477c-956b-4a89-bda0-3665b7a85fff.png">

4. In Blender open a new blend file and delete everything from the scene. 

5. Save the .blend file to the Blend_My_NFTs folder and reload the .blend file from the new directory.

7. Run main.py in the Blender Scripting Tab

The generated 3D models will appear in the folder 3D_Model_Output

## How Rarity works

Rarity is a percentage value and accepts fractions like 0.001%, but they must be specified with decimals in the naming. For ease of use the percentages need to add up to 100%:

```
33% + 33% + 33% + 1% = 100% 

Variant 1 = 33% chance
Variant 2 = 33% chance
Variant 3 = 33% chance
Variant 4 = 1% chance
```

If you have 20 variants with 50 set as the rarity percentage for each, Blend_My_NFTs will add up the percentages then treat the sum as 100%:

```
50% + 50% + 50% + 50% + 50%....
= 1,000%

Out of 100%:

(50/1,000)*100 = 5% chance of 1 variant
```

Rarity is dependent on both the number of NFTs you generate, as well as the maximum number of possible combinations of the attributes in your .blend file. 

This means the following two scenarios, say, at a fixed number of 10,000 NFTs to generate;

1. Your .blend file has 1,000,000,000 possible combinations (trust me that's a small number, our collection for This Cozy Place has over 11 Trillion possible combinations). Generating 10,000 will be more representative of the rarity numbers you set as the script will simply have more combinations to choose from.

2. Your .blend file has 10,000 possible combinations. This means that all possible combinations of your NFT will be generated, meaning that no rarity can be taken into account since the only way to reach your required 10,000 NFTs to generate is by including NFTs that

This is the result for following reasons: 

1. The rarity is determined sudo randomly by, but is weighted based on each variants rarity percentage.

2. The script prioritises the number of NFTs to generate (that you set in config.py with the maxNFTs variable) over rarity percentage

This behaviour is a fundamental mathematical result, not an issue with the code. I've researched various ways at creating and enforcing rarity, this is the only way I have found that works. If you have found a better method, feel free to make a pull request and I'd be happy to review and merge it to the main Github repo for BMNFTs.

The code for that determines rarity can be found in ``src/Main_Generators/Rarity_Sorter.py``. The most important line in that file is ``70``, that is what generates the randomly weighted DNA. After that it is checked by line 

## Helpful Links

This Blender add on heaviliy relies on the Blender API and its documentation which you can find here: https://docs.blender.org/api/current/index.html

If you have no experience with the Blender API I recomend watch this tutorial on running python scripts in Blender: https://www.youtube.com/watch?v=cyt0O7saU4Q 

There is also helpful documentation in the Blender API about running scripts here: https://docs.blender.org/api/current/info_quickstart.html#running-scripts

Note - You might want to install the Icon Viewer add-on for Blender: https://docs.blender.org/manual/en/latest/addons/development/icon_viewer.html 

## Disclaimers

Blend_My_NFTs works with Windows 10 or macOS BigSure 11.6 on Blender 3.0.0. These are the operating systems I have tested the scripts on, I do not garuntee they will work on other operating systems. I do not garuntee this software will work with your setup. There are many variables and factors that go into running the software provided, it differs from system to system, and from blend file to blend file.

I encourage you to do some trouble shooting, read the Blender API documentation, read this tutorial, review the scripts, and do your own research before reaching out for help on our discord. If you are really stuck and are out of options I am available on our disord channel above for consulting. However! I am not a toutor. Although I enjoy teaching people, I simply do not have the time to work, build this project, teach people Blender/Python, and live my life. So please respect my time, I'd love to help! 

To be honest I have no idea how to use Blender. I know some basic things, but I know the API and Python a lot better. This is my first Blender/Python project, so you may be wondering "how is he making a NFT collection with Blender??" Well I'm not, I write the code for the Blend_My_NFTs, and my team has three other members; Devlin and Caelin, who create the scenes and models in Blender, and the third is Quinn who is the lead web developer for our site. 

If building an NFT collection in blender is something you really want to do and you have experience with Blender, I suggest you get familiar with some basic Python functionality and then how to run scripts in the Belnder Text Editor (an indepth knowledge is not required). However, if you don't use Blender but have a coding background, I would suggest watching some basic tutorials just to get a feel for the software (an indepth knowledge is not required).

This tutorial page is not finished! This page will be updated as I commit/merge new changes to the main branch. (Last updated Nov 10th, 2021)

I garuntee this will eventually be an add on to Blender and not just a script you run through the script editor. (I mostly just put this in here for personal motivation, please don't pester me about the date lol)

Nothing in this repository or its documentation is financial advice. If you create an NFT project or collection with Blend_My_NFTs, you do so at your own personal and financial risk. We are only providing a means of acomplishing a goal, not investment or financial information about that goal. Do your own research and come to your own conclusions before spending money on NFTs or any asset for that matter. We are not liable for any finacial losses you may encure while using this software. Any discussion about finances and cryptocurrencies in this repository or its documentation are done with the intent to educate and provide examples to help our users understand concepts relating to Blend_My_NFTs and This Cozy Place. 

The creators of This Cozy Studio will never, under any cricumstance, ask for your crypto wallet(s) secret phrase or private keys. If you come across anyone who is impersonating the founding members of This Cozy Place, please report it immediately to the admins on our discord channel and we will take appropriate action and warn our community of the behaviour. If this takes place outside of our community boundries then report the user to the appropriate authorities. 

This software is provided for free and is open source. We are not liable for any felones you may commit using this software, and we staunchly appose the malicious use of this software that in any way breaks any applicable law in your loction of residence. 

## Donations

Only donate if you are financialy able to, I'm am a well off individual and do not need donations to survive. I do acknowledge some people in our community wish to donate to show their appreciation for the work I've put into this project and I apprieciate the support. 

Cardano (ADA) address: 

addr1q9gh2u4ssptpltl86gy4sspy3naqwfn74zwqcf3k0jmh66xrpv232dnkm46lsf9deqccl3xd2vpyksl6zy5v4r94k0nsw5lnfp


Solana (SOL) address: 

A7NuHB79DKfkdZMvqVzBrYN4NXRqP7LVFjMdVoKRfVmo
