<!---
   Licensed to the Apache Software Foundation (ASF) under one or more
   contributor license agreements.  See the NOTICE file distributed with
   this work for additional information regarding copyright ownership.
   The ASF licenses this file to You under the Apache License, Version 2.0
   (the "License"); you may not use this file except in compliance with
   the License.  You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
-->

# slider-dependency-check

Check slider dependencies with a no-op build that pulls down everything for a chosen version from a staging repository
or the central one.

It currently does nothing with the files; in future some JUnit tests may examine the contents of the packages, especially the `.tar.gz` & `.zip` files to verify they include mandatory files. 

## Usage

1. Either pick a profile or edit the POM to create a new one.
1. OR: edit `build.properties` and set `slider.version=0.71` or similar.
1  Purge the local repository as described below.
1. Run the maven package target, using the `-Pstaging` profile to use the ASF staging repository as the
source of artifacts.
1. If it fails: something didn't get published.

Example:

    mvn clean package -Pstaging

### How to purge the local repository of the artifacts

To delete any local slider packages

    rm -rf ~/.m2/repository/org/apache/slider/

There is a profile, `purge`, bit it does not seem to purge everything.

    mvn package -Ppurge -Pstaging

This will cull the core dependencies of this check (but nothing transient), then run the build against 

## What does it check?

Look at the POM for the list of dependencies. Essentially

1. The core JARs
1. Their test JARs
1. Their source JARs
1. The `-all.zip` file
1. The `-all.tar.gz` file
1. The root slider POM
1. The transient dependencies of these files.


# License


    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
    
     (http://www.apache.org/licenses/LICENSE-2.0)
    
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License. See accompanying LICENSE file.

