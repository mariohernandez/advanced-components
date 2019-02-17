# Component Based Development
Component based development is typically broken down into 3 parts:

1. Building stand-alone components with Twig and Pattern Lab.

2. Building Drupal's back-end (i.e. content types, paragraph types, etc.).

2. Integrating the components with Drupal.

## Local Development Environment Setup

This repo includes everything you need to set up a [Lando-based](https://docs.devwithlando.io/) local Drupal development environment, along with the required front end tools (Node, Pattern Lab, Gulp, etc.). For best results, follow these steps to get your environment setup.

## 1. Install Lando and Docker
Lando is a free, open source, cross-platform, local development environment tool built on Docker container technology.

### System requirements

This is only going to work if you have a fairly new computer. According to the [Lando documentation](https://docs.devwithlando.io/installation/system-requirements.html#operating-system) you will need one of the following:

* macOS 10.10+ \(May need to install command line tools\)
* Windows 10 Pro+ \(or equivalent\) with Hyper-V running
* Linux \(with kernel version 4.x or higher\)

  So far, we have tested only with macOS 10.13 \(High Sierra\) and 10.14 \(Mojave\).

### Run the installer

* [Install Lando and Docker](https://github.com/lando/lando/releases/tag/v3.0.0-beta.47) (v3.0.0-beta.47)

At least on a Mac, this installs Lando along with Docker. Optionally, you can install Docker first: the Lando installer has not been updated with the latest version of Docker.

**IMPORTANT**

* **Docker is required**

  Docker makes it possible to build containers for any of the third party integrations required in your environment. If you already have Docker installed you don't need to install it again as part of Lando's installation.

**NOTE**: If you are using OSX, you may need to install XCode's Command Line Tools.

## 2. Clone this repo anywhere in you local system
* In your preferred terminal app, run the following command:<br />
```git clone git@github.com:mariohernandez/component-based-development.git```

* If you experience issues with the command above, try this one:<br />
```git clone https://github.com/mariohernandez/component-based-development.git```


## 3. After cloning this repo, run the following commands from the root level of the repository:

1. `cd component-based-development`<br />_This is the default directory generated by cloning the repo.  If you changed the directory name when cloning the repo, cd into that directory and run the following commands from it_.

2. `lando start`<br />_This will set up Lando plus pull down Drupal and required contrib modules.  This process could take a few minutes to complete. After following these steps, you will see a list of URLs to access a basic, unstyled Drupal site.  Hold off to clicking any links for now._

3. `lando drush si -y config_installer --account-name=admin --account-pass=admin --db-url='mysql://drupal8:drupal8@database/drupal8'`<br />_This will do a basic installation of Drupal with some custom configuration._

4. `cp -r assets/imgs/. web/sites/default/files/.`<br />_This will copy our sample image assets to the default files directory for your local installation of Drupal._

5. `lando db-import drupal8.export.gz`<br />_This will import a custom database that includes placeholder content for the demo site we'll use in the training exercises._

6. `lando drush cr`<br />_This will clear the Drupal caches._


## 4. Install Front End Tooling including PatternLab

1. `cd web/themes/custom/nitflex_dev_theme`

2. Run: `lando npm install`<br />_This will install the required front end tools (Node, Gulp, etc.)_

3. Move into the patternlab directory:  `cd patternlab`

4. Run: `lando composer install`<br />_This will install PatternLab_<br />
    - If/when prompted that the `path ./../dist/style-guide/ already exists`, reply with **M**.<br />
    - If/when prompted to `update the config option twigAutoescape`, reply with **Y**.<br />
    - If/when prompted to `update the config option styleguideKitPath`, reply with **Y**.

5. Run an initial build of the front end tools and PatternLab.<br />
    1. First, make sure you're at the root level of the theme (`cd ../`),<br />
    2. then run<br />```lando npm run build && lando php patternlab/core/console --generate```

### Login to the site and preview the final results
- Go to: [http://nitflex.lndo.site/user](http://nitflex.lndo.site/user) and log in with username: `admin`, pw: `admin`.

- To access PatternLab, which where our components will be displayed, go to [http://nitflex.lndo.site/themes/custom/nitflex_theme/dist/style-guide/](http://nitflex.lndo.site/themes/custom/nitflex_theme/dist/style-guide/)

# You are done! 🙌 🔥 👊


## Not using Lando?

Although we highly encourage you to use the already tested setup above, you are free to use your existing Drupal development workflow.  This however will require you complete several manual tasks so you can be up to speed and ready to follow along during training.

1. [Download or clone the provided repo](https://github.com/mariohernandez/component-based-development) to access the assets you will need to follow along.

2. Copy **`web/themes/custom/nitflex_dev_theme`** into your own Drupal themes location (i.e. web/themes/custom/).

3. Copy all images from this repo's **`/assets/imgs/`** into your Drupal's files directory (i.e. web/sites/default/files/).

4. Make sure the following modules (plus their dependencies) are installed:
    * [Admin Toolbar](https://www.drupal.org/project/admin_toolbar)
    * [Twig Field Value](https://www.drupal.org/project/twig_field_value)
    * [Devel](https://www.drupal.org/project/devel)
    * [Flag](https://www.drupal.org/project/flag)
    * [Component Libraries](https://www.drupal.org/project/components)
    * [Path Auto](https://www.drupal.org/project/pathauto)
    * [Token](https://www.drupal.org/project/token)
    * [Yaml Content](https://www.drupal.org/project/yaml_content)
    * [Paragraphs](https://www.drupal.org/project/paragraphs)

5. Import **drupal8.export.gz** (found in the root of this repo) into your own Drupal database. **WARNING: this will override your current database**.  This creates all the Drupal infrastructure we need for the training (content types, views, view modes, image styles, etc.), plus some sample content. For more advanced users, you can find site configuration files in `/config/sync/`, but you will be on your own for generating sample content. This would be an extremely time consuming process if you opt to do it by hand so we highly recommend you use the provided database dump.

6. If you successfully followed all the steps, you can login to your site using `admin` and `admin` as username/password.

---
**NOTE**:  This is a full class and assistance with your local environment may be limited. We are leveraging Lando to help streamline the setup of a consistent local development environment.
<!-- TODO: Commenting for now until documentation is complete. -->
<!-- ## Workshop exercises:

[Component based development exercises](https://mariohernandez.gitbooks.io/components-training/). -->
