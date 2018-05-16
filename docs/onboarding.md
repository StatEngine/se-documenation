## Overview

The onboarding process can take a few hours to several weeks depending on the complexity, security, and resources available to support the onboarding process.  We're here to support you along the way, so please reach out to us if you need support!

### 1. Connect Your Data
StatEngine integrates with common fire department data sources including data warehouses, Computer Aided Dispatch (CAD) systems and Records Management Systems (RMS). Multiple approaches, listed below, can be used to securely send data to StatEngine. Your department should review the various approaches and once the desired integration approach is identified, fill our our survey [here](https://docs.google.com/forms/d/e/1FAIpQLSfJKbY42mFT6ZnF-ASkJUOnxcUloF-xYcCIdmKiq2XNqKQHyw/viewform).  

#### Spade
[Spade](https://statengine.io/spade), an application developed by our team, can run on your local network to read data from your local database(s) and send it to StatEngine. Spade can also be configured to run on your local network and watch a directory for CAD files and then push them to NFORS.

#### PulsePoint
If your department has an existing [PulsePoint](http://www.pulsepoint.org/) integration, you can leverage the same integration to send CAD data to StatEngine.

#### Linked Database
If you are able to push data to a database in our cloud environment, we can provide you with connection information to push data to a dedicated database we stand up for you.  This approach minimizes the amount of software that needs to run on a department’s infrastructure, however it requires the local jurisdiction to setup and configure the linked database and synchronization logic.

#### Email
If your database has an email hook, we can setup a secure receiving account to receive, process, and ingest your data.

#### FTP/SFTP
If your database(s) have an FTP/SFTP hook, we already have a secure endpoint that you can push your data to.

#### Custom
Have a more convenient way to push data to us or have an API that we can query, let us know!

### 2. Verify Your Data
Once StatEngine starts receiving data, we will work with you to identify missing or erroneous data. Often times we'll need details on missing apparatus types, battalion and district mappings to enrich your data to the fullest extent.

### 3. Access Your Data
After data verification, we will set you up with a customized [Dashboard](userGuide?id=Dashboard) so you can start exploring your data.

### 4. Explore Your Data Even More
StatEngine has even more ways to add and enrich your data via the [Marketplace](userGuide?id=Marketplace). Explore plugins and apps like adding weather, traffic, or directly tweeting stats to Twitter.
