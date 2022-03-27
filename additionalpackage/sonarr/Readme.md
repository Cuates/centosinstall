Sonarr Configuration

NOTE: To search and retrieve files you must have set up an indexer application first

NOTE: Check to see if show advanced is on
* Settings
  * Media Management
    * Episode Naming
      * Check
        * Rename Episodes
        * Replace Illegal Characters
      * Modify String
        * Standard Episode Format
          * {Series Title} S{season:00} E{episode:00} {Episode Title}
        * Daily Episode Format
          * {Series Title} {Air-Date} {Episode Title}
        * Anime Episode Format
          * {Series Title} S{season:00} E{episode:00} {Episode Title}
        * Series Folder Format
          * {Series TitleYear}
        * Season Folder Format
          * Season {season:00}
        * Specials Folder Format
          * {Series Title} {season:00}
    * Folders
      * Check
        * Delete empty folders
    * Importing
      * Episode Title Required
        * Always
      * Minimum Free Space
        * 100
      * Check
        * Use Hardlinks instead of Copy
    * File Management
      * Propers and Repacks
        * Prefer and Upgrade
      * Check
        * Analyse video files
      * Rescan Series Folder after Refresh
        * Always
      * Change File Date
        * None
      * Recycling Bin Cleanup
        * 7
    * Root Folders
      * path\to\root\folder
  * Profiles
    * Release Profiles
      * English_Translated
        * Name
          * English_Translated
        * Check
          * Enable Profile
        * Must Contain
          * dual
          * dub
          * dual audio
          * dual-audio
          * triple audio
          * triple-audio
          * tri audio
          * tri-audio
          * quad audio
          * quad-audio
          * multi audio
          * multi-audio
        * Must Not Contain
          * lostyears
          * erai-raws
          * -ks-
        * Preferred
          * dual
            * 20
          * dub
            * 10
          * multi
            * 5
          * tri
            * 5
          * quad
            * 5
        * Indexer
          * (Any)
        * Tags
          * dual
          * dub
          * dual-audio
          * triple-audio
          * tri-audio
          * quad-audio
          * multi-audio
      * English_Sub_Japanese_Translated
        * Name
          * English_Sub_Japanese_Translated
        * Check
          * Enable Profile
        * Must Not Contain
          * lostyears
          * erai-raws
          * -ks-
        * Preferred
          * subsplease
            * 20
        * Indexer
          * (Any)
        * Tags
          * sub
      * English_Sub_Chinese_Translated
        * Name
          * English_Sub_Chinese_Translated
        * Check
          * Enable Profile
        * Must Contain
          * vipapkstudios
          * bluesilversect
        * Indexer
          * (Any)
        * Tags
          * esubct
      * TV_Audio_Encode
        * Name
          * TV_Audio_Encode
        * Check
          * Enable Profile
        * Must Contain
          * dd5.1
          * dd7.1
          * ddp5.1
          * ddp7.1
          * dts-hd.ma.5.1
          * dts-hd.ma.7.1
          * truehd.5.1
          * truehd.7.1
        * Preferred
          * ddp5.1
            * 20
          * ddp7.1
            * 15
          * dd5.1
            * 5
          * dd7.1
            * 5
          * dts-hd.ma.5.1
            * 10
          * dts-hd.ma.7.1
            * 5
          * truehd.5.1
            * 5
          * truehd.7.1
            * 5
        * Indexer
          * (Any)
        * Tags
          * tvaudioencode
      * TV_Stream_Source
        * Name
          * TV_Stream_Source
        * Check
          * Enable Profile
        * Must Contain
          * amzn
          * dsnp
          * hmax
          * hulu
          * nf
          * sho
        * Indexer
          * (Any)
        * Tags
          * tvstreamsource
      * Video_Encode
        * Name
          * Video_Encode
        * Check
          * Enable Profile
        * Must Contain
          * h264
          * h265
          * h266
          * x264
          * x265
          * x266
        * Indexer
          * (Any)
        * Tags
          * videoencode
  * Quality
    * 1080p
      * Size Limit
        * Slide the bar to the farthest it can go to the right
      * Excluding
        * HDTV-1080p
  * Download Clients
    * + (plus) button
      * Torrents
        * Select torrent client of choice
        * Name
          * torrent_client_downloader_sonarr
        * Check
          * Enable
        * Host
          * localhost OR hostname
        * Port
          * 8080 OR port number
        * Category
          * sonarr name to be seen on torrent client
        * Completed Download Handling
          * Check
            * Remove Completed
        * Click Test button
          * If all is good, click Save button
    * Completed Download Handling
      * Check
        * Enable
        * Redownload Failed
  * UI
    * Calendar
      * First Day of Week
        * Sunday
      * Week Column Header
        * Tue 3/25
    * Dates
      * Short Date Format
        * 2014-03-25
      * Long Date Format
        * Tuesday, March 25, 2014
      * Time Format
        * 17:00/17:30
      * Check
        * Show Relative Dates
