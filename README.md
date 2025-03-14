# Solr & Drupal Search Setup Guide 🔍

This guide will help you set up **Apache Solr** with **Drupal** using the **Search API** module. Follow these steps to install, configure, and integrate Solr for high-performance search.

## Prerequisites
- A working **Drupal 10** site (**DDEV, Lando, or local setup**)

---

## Install Solr

#### Local Setup (Non-Docker Installation)
If you are **not using a Docker-based installation**, follow these steps:

1. Go to the **Solr download page**: [https://solr.apache.org/downloads.html](https://solr.apache.org/downloads.html)
2. Download the **Binary releases**.
3. Unzip the downloaded file ang go to 'bin'.
4. Start Solr from the command line:
   ```sh
   solr start
   ```
To Check to Solr Admin Interface go to http://localhost:8983/solr/#/

### Install and Enable Search API and Solr Search API Modules

✅ [Search API Module](https://www.drupal.org/project/search_api)
✅ [Search API Solr Module](https://www.drupal.org/project/search_api_solr)

To integrate Solr with Drupal, install the required modules using Composer:

```sh
composer require drupal/search_api drupal/search_api_solr
drush en search_api search_api_solr -y
```

### Configure Solr Server in Drupal

To connect Solr with Drupal, follow these steps:

1. Navigate to **Search API Configuration**:  
   Go to:  /admin/config/search/search-api
2. Click **"Add Server"** and fill in the following details:

- **HTTP Protocol**: `http`
- **Solr Node**: `solr`
- **Solr Port**: `8983`
- **Solr Path**: `/`
- **Solr Host Context**: `solr`

3. Save the configuration.
4. Go to : admin/config/search/search-api/server/YOUR_SERVER_NAME
5. export config using "Get config.zip" button and unzip.
6. Now go to the Solr Admin Interface and click "Core Admin"
7. Click "Add core" and fill up the form.
8. The name sould be the same you added in the Search API config file and hit add core.
9. You will see an error message regarding the missing files. Now go to the Solr folder, [/server/solr/THE-CORE-NAME]
10. Create a folder 'conf'
11. Paste the config files you exported from "Get config.zip".
12. Now Go to the server page, you should see "The Solr server could be reached."
This will connect your Drupal site to Solr successfully. 🚀🚀🚀

### Create Index
1. Using the Manage administrative menu, navigate to Configuration > Search and Metadata > Search API.
2. Click Add Index.
3. Enter an Index Name of your choosing.For Datasources, select Content.
4. Scroll down and select the Server you created earlier.
5. Press Save.
### Add fields
1. Using the Manage administrative menu, navigate to Configuration > Search and Metadata > Search API.
2. Locate the index you created earlier and open it for editing.
3. Open the Fields tab.
4. Click Add fields.
5. The Add fields to index... modal dialog appears.
6. Click save
### Populate Search API Indexes
1. Using the Manage administrative menu, navigate to Configuration > Search and Metadata > Search API.
2. Under the Name column, click the link for the Search API index you need to reindex.
3. A new page appears. Notice the progress bar at the top; this indicates how many nodes have been indexed, and how many remain to be indexed.
4. Click Index now.
     Drush command to reindex the site:
```sh
   drush sapi-i
```

### Create a Search API View to Display Results
1. Go to **Structure > Views** (`/admin/structure/views`).
2. Click on **"Add view"**.
3. Enter a **View name** of your choice.
4. Under **View settings**, select **Show: Index your_index_name**  
   *(Replace `your_index_name` with the actual name of your Search API index.)*
5. Choose **Create a page**, and configure the display settings as needed.
6. Click **Save and exit** to finalize the view.

### Preprocessors
1. Navigate to Configuration > Search and Metadata > Search API (admin/config/search/search-api).
2. Edit the index to which to add the processor.
3. Open the Processors tab.
4. Read through the list of processors, selecting one or more for use. for example, 'content access', 'Highlight'.

### Autocomplete
1. Install the following module and enable it
```sh
   composer require 'drupal/search_api_autocomplete:^1.10'
```
2. Select the search view from the config.
   
### Spell Check
1. Install the following module and enable it
```sh
composer require 'drupal/search_api_spellcheck:^4.0'
```
2. Select the field and change assign type to 'spellcheck'.
3. In the view, add header for spell check.
   
### Facets 🎯
1. Install the following module and enable it
```sh
composer require drupal/facets
drush en -y facets
drush cr
```

3.  Go to Configuration → Search and Metadata → Facets.
4. Click Add Facet.
5. Fill in the details:

    Facet Name: Enter a descriptive name (e.g., "Categories").
    Facet Source: Select the Search API view you created.
    Facet widget: Choose the display type (e.g., Checkboxes, Dropdown, Links).

6. Click Save and Continue.
7. Place the Facet in the Block
    Navigate to Structure → Block Layout.
    Locate the region where you want the facet filter to appear.
    Click Place Block and search for your newly created Facet block.
8. Save and check.
   
