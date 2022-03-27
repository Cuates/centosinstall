Prowlarr Configuration

NOTE: To search and retrieve files you must add indexers first
* Indexers
  * + Add Indexer
    * Search and or choose indexers of choice

NOTE: Check to see if show advanced is on
* Settings
  * Apps
    * + &#40;plus&#41; button
      * Add Application
        * Select application client of choice
          * If you select Sonarr, then you must set up Sonarr first
      * Name
          * Name of application
      * Sync Level
        * Add and Remove Only
      * Prowlarr Server
        * http://localhost:9696
      * Sonarr Server
        * http://localhost:8989
      * ApiKey
        * Copy and Paste applications ApiKey
          * Located in Sonarr's UI settings
            * Settings > General > Security > API Key
      * Click Test button
        * If all is good, click Save button
  * Download Clients
    * &#43; (plus) button
      * Torrents
        * Select torrent client of choice
        * Name
          * torrent_client_downloader_prowler
        * Check
          * Enable
        * Host
          * localhost OR hostname
        * Port
          * 8080 OR port number
        * Category
          * prowlarr name to be seen on torrent client
        * Click Test button
          * If all is good, click Save button
  * UI
    * Dates
      * Short Date Format
        * 2014-03-25
      * Long Date Format
        * Tuesday, March 25, 2014
      * Time Format
        * 17:00/17:30
      * Check
        * Show Relative Dates
    * Language
      * UI Language
        * English
