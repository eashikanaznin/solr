# Solr & Drupal Search Setup Guide

Solr & Drupal Search Setup Guide
This guide will help you set up Apache Solr with Drupal using the Search API module. Follow these steps to install, configure, and integrate Solr for high-performance search.

Prerequisites
- A working Drupal 10 site (DDEV, Lando, or local setup)

Install Solr
	- Local set up [If you are not using docker based installation]
	- Go to Solr download page: https://solr.apache.org/downloads.html
	- Download the Binary releases
	- Unzip
	- Form commad line start Solr using the following command
		○ solr start

Install and enable Search API and Solr Search API module
In order to integrate Solr with Drupal, Download and Install the following modules
	- Composer command
		○ composer install drupal/search_api
		○ composer install drupal/solr_search_api
		○ drush en  search_api, solr_serach_api

Add Server
 - Go to '/admin/config/search/search-api'
	- Click "Add Server"
	- Fill up the form
		○ HTTP protocol: http
		○ Solr node: solr
		○ Solr port: 8983
		○ Solr path: /
		○ Default Solr collection: techproducts (You can define any name here. The collection will be created automatically.)
		○ Solr host context: solr
		
Install Solr(With DDEV)
	
- Apache Solr installed (Recommended: Solr 8.x or 9.x)
- Search API and Search API Solr modules installed
2. Installing Solr
Option 1: Using DDEV (Recommended)
Run the following command to start Solr in DDEV:
ddev get ddev/ddev-solr
Option 2: Using Lando
Add Solr to your .lando.yml file:
services:
solr:
type: solr
core: drupal
Then run:
lando rebuild -y
lando start
3. Configuring Solr in Drupal
1. Enable the Search API and Search API Solr modules:
ddev drush en search_api search_api_solr -y
2. Go to Configuration -> Search API -> Add Server.
3. Choose 'Solr' as the backend and enter the Solr connection URL (e.g.,
http://localhost:8983/solr/drupal).
4. Save and verify the connection.
4. Creating a Search Index
1. Go to Configuration -> Search API -> Add Index.
2. Name the index and choose 'Content' as the data source.
3. Select 'Solr Server' as the backend.
4. Add important fields like Title, Body, and Tags.
5. Save the index and start indexing content:
ddev drush search-api:index
5. Creating a Search Page with Views
1. Go to Structure -> Views -> Add New View.
2. Choose 'Search API index' as the data source.
3. Add fields: Title, Body, Author.
4. Add a Fulltext Search filter.
5. Save the view and test your search.
6. Adding Faceted Search
1. Enable the Facets module:
ddev drush en facets -y
2. Go to Structure -> Facets -> Add Facet.
3. Choose 'Tags' as the facet field.
4. Select 'Block' for display.
5. Save and place the block in the sidebar.
7. Troubleshooting & Best Practices
- Ensure Solr is running: ddev exec solr status
- If indexing fails, clear the index: ddev drush search-api:clear
- Boost fields in Search API settings to improve relevance.
![image](https://github.com/user-attachments/assets/7a7f1156-7699-47c8-b0ee-34387083214e)
