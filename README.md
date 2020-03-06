# Overview

Cohesion Basic is an experimental set of modules, features and config which automates some of the Cohesion installation and configuration steps.

At a high level, it provides:
- `Cohesion Page` content type, which can be used to create pages and place Cohesion components on them. You could create a campaign, landing or even homepage using this content type.
- `Cohesion block` block type, which can be used to create blocks and place Cohesion components on them. You could create a Footer or a Header block and use it on different pages of your site.
- Sub-modules to import the [UI Kit](https://uikit.cohesiondx.com/), which provides a rich set of common webpage components.
- Required [theme changes](https://cohesiondocs.acquia.com/user-guide/step-3-modify-your-website-theme) without modifications of your existing Drupal theme code.
- A simple Image Browser for sites which do not have one already.


# Set up instructions

## Preparing your codebase

To prepare your codebase for Cohesion follow [instructions](https://cohesiondocs.acquia.com/user-guide/step-1a-installing-acquia-cohesion-modules-your-website-composer) on [Acquia Cohesion User Guide](https://cohesiondocs.acquia.com/user-guide)

Skip step "5. Enable Acquia Cohesion" for now. Cohesion Basic will enable the modules for you.

After Cohesion modules are added, add the `cohesion_basic` module to modules/custom folder or run:
```
composer config repositories.cohesion_basic vcs https://github.com/alexku/cohesion_basic
composer require alexku/cohesion_basic:dev-master
```

If your site does not have an Image Browser and you will want to use simple Image Browser from `cohesion_basic_media` module, run this command:
```
composer require drupal/views_infinite_scroll
```

## Enabling modules and configuring your site

1. Enable `cohesion_basic` module.
1. Configure Cohesion keys on page /admin/cohesion/configuration/account-settings
1. Configure image browsers on page /admin/cohesion/configuration/system-settings
  1. Enable `cohesion_basic_media` module to get a simple Drupal core media based image browser configured.
1. Configure the Color palette: /admin/cohesion/cohesion_website_settings/color_palette/bulk_edit and other styling settings to align cohesion styling with main website theme. Check [this page](https://cohesiondocs.acquia.com/user-guide/using-acquia-cohesion-existing-website) for additional instruction.
1. Enable `cohesion_uikit_mobilefirst` **OR** `cohesion_uikit_desktopfirst` module to import the UI kit and disable master templates. The module will import significant amount of config and it is best to enable the module separately from other modules. **Do not** enable both modules at the same time.
1. Rebuild Cohesion: /admin/cohesion/developer/rebuild

1. Create a page: /node/add/cohesion_canvas_page or a block: /block/add/cohesion_canvas_block

## Additional features


### Theme switching

If you install the [Theme Switcher Rules](https://www.drupal.org/project/theme_switcher) module, Cohesion Basic will add an example theme switcher rule.

The rule is disabled by default. Once enabled it will switch site theme to `cohesion_theme` on all `cohesion_page` node pages.

Rules are configured on page: /admin/config/system/theme_switcher

Theme switching allows you to create standalone "micro-site" or "campaign" type pages, which have to look differently than the rest of the site.



# Known issues

1. Dependency on the `features` module. Config import by `cohesion_uikit_mobilefirst` and `cohesion_uikit_desktopfirst` modules has problems without `features` module.
1. UI Kit components imported from features are missing preview / thumbnail images.
1. Import of UI Kit results in translation related warnings / errors.
1. If your custom theme is configured to be used as default site theme and administration theme at the same time, Cohesion styles (CSS) will not be added correctly.


# Ideas to implement

1. Hiding regions or switching theme from cohesion_canvas_page content type.
1. `cohesion_basic_media` module could set the Cohesion image browser setting, if there is no image browser configured.
1. Nodes with Cohesion components added to a site using blocks can allow preview and moderation of site header and footer.
1. `cohesion_basic` module currently sets `cohesion: true` and adds the `<cohesion-placeholder>` tag to all enabled themes. We could provide a configuration form to choose which themes should be modified.
