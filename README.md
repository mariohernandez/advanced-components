# Component Based Development in Drupal 8
The component based development training is broken down into 3 parts:

1. Building stand-alone components in Twig using KSS Node.

2. Building Drupal's back-end.

2. Integrating the components with Drupal.

## Local Development Environment Setup

This repo includes everything you need to set up a [Lando-based](https://docs.devwithlando.io/) local develop environment of Drupal, along with the required front end tools (Node, Gulp, etc.) For best results, follow these steps for completing the setup of your local development environment.

### 1. Install Lando, along wth dependencies (Docker).
Lando is a free, open source, cross-platform, local development environment tool built on Docker container technology. See the documentation [https://docs.devwithlando.io/installation/installing.html](https://docs.devwithlando.io/installation/installing.html)

**NOTE**: If you are using OSX, you may need to install XCode's Command Line Tools.

### 2. Clone the training repository anywhere in you local system.
`git clone git@github.com:mariohernandez/component-based-development.git`

### 3. After cloning this repo locally, run the following commands from the root level of the repository in your preferred terminal app:

- `cd component-based-development`

- `lando start`<br />_This will set up Lando, plus pull down Drupal and required contrib modules._

- `lando drush si -y config_installer --account-name=admin --account-pass=admin --db-url='mysql://drupal8:drupal8@database/drupal8'`<br />_This will do a basic installation of Drupal with some custom configuration._

- `cp -r assets/imgs/. web/sites/default/files/.`<br />_This will copy our sample image assets to the default files directory for your local installation of Drupal._

- `lando db-import drupal8.export.gz`<br />_This will import a custom database that includes placeholder content for the demo site we'll use in the training exercises._

- `lando drush cr`<br />_This will clear the Drupal caches._

After following these steps, you should have an unstyled Drupal site available locally at: http://nitflex.lndo.site:8000/<br />_Depending on your setup, you may not need port `:8000`)_

### Install Front End Tooling

- `cd web/themes/custom/nitflex_dev_theme`

- Run: `lando npm install`<br />_This will install the required front end tools (Node, Gulp, etc.)_

### Log into the site and preview the final results
- Go to: [http://nitflex.lndo.site:8000/user](http://nitflex.lndo.site:8000/user) and log in with username: `admin`, pw: `admin`.<br />**IMPORTANT**: _Your Drupal site URL my be different.  In some instances the `:8000` part of the URL is not needed_.

<!-- Removing this for now.  We may just do a demo during training of the complete theme. -->
<!-- - Go to: [http://nitflex.lndo.site:8000/admin/appearance](http://nitflex.lndo.site:8000/admin/appearance) and set the default theme to be the **Nitflex** theme. Return to the homepage.
- You should now see a styled version of the site! Switch the site back to the Nitflex **DEV** theme, and now let's get crackin' making it look as pretty as the finished Nitflex theme! -->

**NOTE**:  This is a full class and assistance with your local environment may be limited. We are leveraging Lando to help streamline the setup of a consistent local development environment.


## Not using Lando?

Although we highly encourage you to use the already tested setup above, you are free to use your existing Drupal development workflow.  This however will require you complete several manual tasks so you can be up to speed and ready to follow along during training.

1. [Download or clone the provided repo](https://github.com/mariohernandez/component-based-development) to access the assets you will need to follow along.

2. Copy **`web/themes/custom/nitflex_dev_theme`** into your own Drupal themes location (i.e. web/themes/custom/).

3. Copy all images from this repo's **`/assets/imgs/`** into your Drupal's files directory (i.e. web/sites/default/files/).

4. Make sure the following modules are installed:
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

<!-- TODO: Commenting for now until documentation is complete. -->
<!-- ## Workshop exercises:

[Component based development exercises](https://mariohernandez.gitbooks.io/components-training/). -->
