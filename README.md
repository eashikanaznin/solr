# Solr & Drupal Search Setup Guide

This guide will help you set up **Apache Solr** with **Drupal** using the **Search API** module. Follow these steps to install, configure, and integrate Solr for high-performance search.

## Prerequisites
- A working **Drupal 10** site (**DDEV, Lando, or local setup**)

---

## Install Solr

### Local Setup (Non-Docker Installation)
If you are **not using a Docker-based installation**, follow these steps:

1. Go to the **Solr download page**: [https://solr.apache.org/downloads.html](https://solr.apache.org/downloads.html)
2. Download the **Binary releases**.
3. Unzip the downloaded file ang go to 'bin'.
4. Start Solr from the command line:
   ```sh
   solr start
## Install and Enable Search API and Solr Search API Modules

- [Search API Module](https://www.drupal.org/project/search_api)
- [Search API Solr Module](https://www.drupal.org/project/search_api_solr)

To integrate Solr with Drupal, install the required modules using Composer:

```sh
composer require drupal/search_api
composer require drupal/search_api_solr
drush en search_api search_api_solr -y

