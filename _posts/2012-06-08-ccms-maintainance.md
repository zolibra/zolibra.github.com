---
layout: post
title: "CCMS maintainance"
description: ""
category: 
tags: [CCMS, WORK, ClearCase]
---
{% include JB/setup %}
Force a Build
--------------

take pin_sdk in bj_cs3444 for example:
in CCMS command-line:

    setview_cs bj_cs3444
    cd /vobs/isg/devenv/bin

vi and edit the build_ctl file, add one line in the last line:

    force pin_sdk

then save as it as build_ctl.once by :

    :w build_ctl.once

after that you can schedule a build to do this force build.

Change the build Tag:
------------------

take bj_cs3444 for example, first of all, check-out the build_ctl file:

    setview_cs bj_cs3444
    cd /vobs/isg/devenv/bin
    cleartool co -nc build_ctl

edit build_ctl in vi, change Patch=FR2CD2 and  replace FR2CD2 to a new one, save it and check in:

    cleartool ci -nc  build_ctl

after that you can schedule a build to do this build.
