---
title: Oyranos/Configuration Dialog
permalink: wiki/Oyranos/Configuration_Dialog/
layout: wiki
tags:
 - Oyranos
---

The <b> oyranos-config-fltk</b> configuration dialog gives hints, what
options and meta options should be considered in a colour managed
workflow.

Policy
------

|                                                                                |                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](Oyranos-config-flu-0.1.5_policy.png "Oyranos-config-flu-0.1.5_policy.png") | Here the user configures Oyranos the most simple way. He needs to identify her-/himself and choose the appropriate policy setting. Many options in Oyranos are affected by the policy setting. The active policy can been seen on the bottom of the dialog. |
||

Directory Paths
---------------

|                                                                              |                                                                                                                                                                                                                                                           |
|------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](Oyranos-config-flu-0.1.5_paths.png "Oyranos-config-flu-0.1.5_paths.png") | Paths can be configured and freely chosen as many as one needs. Use the big plus button for. The defaults for the profile home, system and Oyranos configuration paths are always included. They are none dependent from policies but may influence them. |
||

Default Profiles
----------------

|                                                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](Oyranos-config-fltk-0.1.5_default-profiles.png "Oyranos-config-fltk-0.1.5_default-profiles.png") | Default profiles act as finer grained preferences than policies and can be considered advanced options. Individually for each case profiles can be selected, which fit the need of a user. The profiles are searched in the previous paths including the standard paths. Changing options here may invalidate a previous selected policy. Use the right hand botton to show the selected profile detailed in ICC Examin (if installed). |
||

Behaviour
---------

### Rendering Intent

|                                                                                                            |                                                                                                                                                                                                                                  |
|------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](Oyranos-config-fltk-0.1.5_behaviour-rendering.png "Oyranos-config-fltk-0.1.5_behaviour-rendering.png") | The behaviour tabs can be considered advanced options. The rendering intent and blackpoint compensation influences the kind of profile build-in gamut mappings. Changing options here may invalidate a previous selected policy. |
||

### Colour Space Mismatch

|                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](Oyranos-config-fltk-0.1.5_behaviour-mismatching.png "Oyranos-config-fltk-0.1.5_behaviour-mismatching.png") | The behaviour tabs can be considered advanced options. The mismatch options help to setup rules for automatic reacting on user behalf. Here will be decided what to do with a undescribed colour space of a image. Or decide here if to convert during editing to editing colour space if not matching with the images native colour space. For most control the user can here switch to 'promt' to pop-up a dialog with further options what to do. Changing options here may invalidate a previous selected policy. |
||

### Proofing

|                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](Oyranos-config-fltk-0.1.5_behaviour-proofing.png "Oyranos-config-fltk-0.1.5_behaviour-proofing.png") | The behaviour tabs can be considered advanced options. The proofing options let the user select a proofer profile and rendering intent. A proofer is used to simulate a other device, for instance a desktop printer on screen or a offset machine on a desktop printer. Here will be decided if proofing is on by default to match the intended device. Changing options here may invalidate a previous selected policy. |
||

### Mixed Colour Spaces in one Document

|                                                                                                    |                                                                                                                                                                                                                                                                                                    |
|----------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![](Oyranos-config-fltk-0.1.5_behaviour-mixed.png "Oyranos-config-fltk-0.1.5_behaviour-mixed.png") | The behaviour tabs can be considered advanced options. These settings influence how to handle mixed colour spaces in one document. Such mixed colour space documents can cause several misbehaviour in later steps of a workflow. Changing options here may invalidate a previous selected policy. |
||

[back -&gt; Oyranos](/wiki/Oyranos "wikilink")
