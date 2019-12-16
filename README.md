# EM Theme Migration
## Objectiv

The goal is either to transfer the theme to the current page, or to play the articles of the old page in the new thenme.

## Plus Ultra

* Get your Local Environment u8 and running
* Include your Repository  (Platform.sh - master branch - dzw)
* Import Database (dzw - production)
    * `Drush cr`
    * Check for tmp errors and fix them
    * Add Debbugging Settings to settings.php if not available yet.
 ```
$config['system.performance']['css']['preprocess'] = FALSE;
$config['system.performance']['js']['preprocess'] = FALSE;
$config['system.logging']['error_level'] = 'verbose';```
    * Disable Aggregation
	* Get new composer.json
	
    
```
    {
        "name": "burdamagazinorg/thunder-project",
        "description": "Project template for Thunder projects with composer",
        "type": "project",
        "license": "GPL-2.0-or-later",
        "authors": [
            {
                "name": "Daniel Bosen",
                "email": "daniel.bosen@burda.com"
            },
            {
                "name": "Christian Fritsch",
                "email": "christian.fritsch@burda.com"
            },
            {
                "name": "Mladen Todorovic",
                "email": "mladen.todorovic@burda.com"
            },
            {
                "name": "Timo Welde",
                "email": "welde@galaniproject.de"
            },
            {
                "name": "Volker Killesreiter",
                "email": "killesreiter@burda.com"
            }
        ],
        "repositories": [
            {
                "type": "composer",
                "url": "https://packages.drupal.org/8"
            },
            {
                "type": "composer",
                "url": "https://asset-packagist.org"
            },
            {
                "type": "package",
                "package": {
                    "name": "heiseonline/shariff",
                    "version": "3.0.1",
                    "type": "drupal-library",
                    "dist": {
                        "url": "https://github.com/heiseonline/shariff/releases/download/3.0.1/shariff-3.0.1.zip",
                        "type": "zip"
                    },
                    "require": {
                        "composer/installers": "^1.2.0"
                    }
                }
            },
            {
                "type": "package",
                "package": {
                    "name": "custom-asset/masonry",
                    "version": "3.3.2",
                    "type": "drupal-library",
                    "dist": {
                        "url": "https://npmcdn.com/masonry-layout@3.3.2/dist/masonry.pkgd.min.js",
                        "type": "file"
                    },
                    "require": {
                        "composer/installers": "^1.2.0"
                    }
                }
            }
        ],
        "require": {
            "burdamagazinorg/thunder": "~8.2",
            "cweagans/composer-patches": "^1.6",
            "drupal-composer/drupal-scaffold": "^2.2",
            "drupal/console": "^1.2",
            "composer/installers": "^1.2",
            "drush/drush": "~8.0|^9.0.0-beta8",
            "oomphinc/composer-installers-extender": "^1.1",
            "webflo/drupal-finder": "^1.0.0",
            "webmozart/path-util": "^2.3",
            "drupal/devel": "^2.0",
            "drupal/superfish": "^1.2",
            "drupal/views_rss": "2.x-dev",
            "drupal/webforms": "0.x-dev",
            "drupal/dfp": "^1.0@alpha",
            "drupal/fontawesome": "^2.9",
            "drupal/custom_pub": "^1.0@alpha",
            "drupal/field_formatter": "^1.2",
            "drupal/masonry": "^1.0@RC",
            "drupal/masonry_views": "^1.0@RC",
            "drupal/page_manager": "^4.0@beta",
            "drupal/panelizer": "^4.1",
            "drupal/panels": "^4.3",
            "drupal/poll": "^1.2",
            "drupal/realname": "^1.0@RC",
            "drupal/slick_views": "^1.0",
            "drupal/views_infinite_scroll": "^1.5",
            "npm-asset/imagesloaded": "^4.1",
            "custom-asset/masonry": "^3.3",
            "heiseonline/shariff": "^3.0",
            "drupal/tb_megamenu": "1.x-dev",
            "drupal/config_delete": "^1.7",
            "drupal/backup_migrate": "^4.0"
        },
        "require-dev": {
            "webflo/drupal-core-require-dev": "^8.4"
        },
        "replace": {
            "bower-asset/shariff": "*"
        },
        "minimum-stability": "dev",
        "prefer-stable": true,
        "autoload": {
            "psr-4": {
                "DrupalProject\\composer\\": "scripts/composer/"
            }
        },
        "scripts": {
            "drupal-scaffold": "DrupalComposer\\DrupalScaffold\\Plugin::scaffold",
            "pre-install-cmd": [
                "DrupalProject\\composer\\ScriptHandler::checkComposerVersion"
            ],
            "pre-update-cmd": [
                "DrupalProject\\composer\\ScriptHandler::checkComposerVersion"
            ],
            "post-install-cmd": [
                "DrupalProject\\composer\\ScriptHandler::createRequiredFiles"
            ],
            "post-update-cmd": [
                "DrupalProject\\composer\\ScriptHandler::createRequiredFiles"
            ]
        },
        "extra": {
            "installer-types": ["npm-asset", "bower-asset"],
            "installer-paths": {
                "web/core": ["type:drupal-core"],
                "web/libraries/masonry": ["custom-asset/masonry"],
                "web/libraries/{$name}": [
                    "type:drupal-library",
                    "type:npm-asset",
                    "type:bower-asset"
                ],
                "web/modules/contrib/{$name}": ["type:drupal-module"],
                "web/profiles/contrib/{$name}": ["type:drupal-profile"],
                "web/themes/contrib/{$name}": ["type:drupal-theme"],
                "drush/contrib/{$name}": ["type:drupal-drush"]
            },
            "patches": {
                "drupal/page_manager": {
                    "2752227: Incorrect page_title title in browser toolbar": "https://www.drupal.org/files/issues/2018-10-26/page_manager-incorrect-page_title-2752227-37-8.x.4.x.patch"
                },
                "drupal/panels": {
                    "2869412: Page title does not display": "https://www.drupal.org/files/issues/2018-03-19/panels--page_title_does_not_display--2869412-27.patch"
                }
            },
            "enable-patching": true
        },
        "config": {
            "bin-dir": "bin/"
        }
    }
```

* `composer install && composer update --with-dependencies`
* `drush updb`
* copy em theme directorys to your new custom theme directory
* copy em custom modules directory to your new custom modules directory
* Disable **malfunctional** configs
```
    drush config-delete -y block.block.breadcrumbs &&
    drush config-delete -y block.block.mainnavigation &&
    drush config-delete -y block.block.mainnavigation_2 &&
    drush config-delete -y block.block.mainpagecontent &&
    drush config-delete -y block.block.tabs &&
    drush config-delete -y block.block.infinite_sub_4channelpresenter &&
    drush config-delete -y block.block.infinite_sub_breadcrumbs &&
    drush config-delete -y block.block.infinite_sub_fussbereich &&
    drush config-delete -y block.block.infinite_sub_headermediablock &&
    drush config-delete -y block.block.infinite_sub_lazyloadingsimple &&
    drush config-delete -y block.block.infinite_sub_mainnavigation &&
    drush config-delete -y block.block.infinite_sub_mainnavigation_2 &&
    drush config-delete -y block.block.infinite_sub_mainpagecontent &&
    drush config-delete -y block.block.infinite_sub_messages &&
    drush config-delete -y block.block.infinite_sub_modalsearch &&
    drush config-delete -y block.block.infinite_sub_newsletterblock &&
    drush config-delete -y block.block.infinite_sub_newsletterlargemenblock &&
    drush config-delete -y block.block.infinite_sub_poweredbythunder &&
    drush config-delete -y block.block.infinite_sub_primaryadminactions &&
    drush config-delete -y block.block.infinite_sub_sidebarblocktest &&
    drush config-delete -y block.block.infinite_sub_sidebarmain &&
    drush config-delete -y block.block.infinite_sub_sidebarmain2 &&
    drush config-delete -y block.block.infinite_sub_sidebarmain3 &&
    drush config-delete -y block.block.infinite_sub_socialsblock &&
    drush config-delete -y block.block.infinite_sub_socialsblock_2 &&
    drush config-delete -y block.block.infinite_sub_tabs &&
    drush config-delete -y block.block.infinite_sub_testtest &&
    drush config-delete -y block.block.infinite_sub_themelogoblock &&
    drush config-delete -y block.block.infinite_sub_veranstaltungdesmonatsnewsroll &&
    drush config-delete -y block.block.infinite_sub_views_block__infinite_channel_presenter_presenter &&
    drush config-delete -y block.block.infinite_sub_views_block__related_articles_block_1
```
* Enable modules needed by em


```bash
drush en -y hal comment content_moderation contextual layout_discovery serialization statistics workflows config_delete ctools_block custom_pub default_content devel kint field_formatter masonry masonry_views page_manager page_manager_ui panelizer panels panels_ipe poll realname scheduler_content_moderation_integration slick_ui slick_views tb_megamenu views_infinite_scroll views_rss_format views_rss em_default_content em_thunder_demo em_dynamic_teaser em_tweaks
```

ConfigImport Exception: 
> If applicable, correct errors manually



* import config files `drush cim -y --partial --source=dir_to_files` from `https://github.com/Coheed/em_config_import` add dont replace
!! **if base_path is unset  workaround - fix** - `add your url to themes/custom/em/include/theme_variables.inc  (could be fixed automaticaly on remote)   $variables['base_path']=$_SERVER['HTTP_HOST'];`

## Last Impediment:
> RuntimeException: Controller "Drupal\page_manager\Controller\PageManagerController::pageTitle()" requires that you provide a value for the "$page_manager_page_variant" argument. Either the argument is nullable and no null value has been provided, no default value has been provided or because there is a non optional argument after this one. in <em class="placeholder">Symfony\Component\HttpKernel\Controller\ArgumentResolver-&gt;getArguments()
