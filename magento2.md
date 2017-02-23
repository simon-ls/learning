# Magento 2

Courses to do:
1. Magneto U: Responsive Web Design in Magneto 2
2. Magento U: CORE PRINCIPLES FOR THEMING IN MAGENTO 2 (FE)
3. http://alanstorm.com/magento-2-frontend-files-serving/

## 1. Default Themes
### 1.1 Blank theme
* The theme uses these breakpoints:
    * `320px`
    * `480px`
    * `640px`
    * `768px` (switches from mobile to desktop)
    * `1024px`
    * `1440px`
* The mobile and desktop styles are defined in separate files:
    * `styles-m.less` is used to generate basic and mobile styles
    * `styles-l.less` is used to generate desktop-specific styles (high than 768px)
    * Only the `style-m.less` is loaded on a mobile device
    * `web/css/source/_module.less` and other less files are outputted to the `styles-m.css` and `styles-l.css` files

### 1.2 UI Library
* Provides the ability to customise and reuse a wide range of elements
* The library includes mixing for arranging RWD styles
* These include breadcrumb, typography, rating, forms, buttons, tabs etc

### 1.3 RWD in Luma
* Uses a mobile first approach
* Your theme should inherit from the “Blank” theme, Luma does this as well
* Styles are compiled into `/pub/static/frontend/Magento/luma/en_US/css/styles-m.css`


## 2. Creating Theme
### 2.1 Paths
1. Theme directory
    * Usually: `app/design/frontend/Magento/<theme>`
    * `vendor/magento/theme-frontend-<theme>`
2. Module directory
    * Usually: `app/code/Magento/<Module>`
    * `vendor/magento/module-<module>-<name>`
    * `<Magento_Checkout_module_dir>`

### 2.2 Creating a storefront theme
1. Create a directory: `app/design/frontend/<vendor>/<theme>`
2. Add a `theme.xml`, `etc/view.xml`, `composer.json`, `registration.php`
3. Store other files in custom directories all under web. In the `.../<theme>/web/images` you store the general theme related static files. For example, a theme logo is stored in ...<theme>/web/images.
4. Configure in admin
5. You will need to clear the cache, and maybe run `grunt clean:<theme-name>`

### 2.3 Theme logo
1. `<theme_dir>/web/images/logo.svg` will be used by default
2. Or it can be overwritten in layout: `<theme_dir>/Magento_Theme/layout/default.xml`

### 2.4 Theme Structure
1. See full table here: http://devdocs.magento.com/guides/v2.1/frontend-dev-guide/themes/theme-structure.html
2. `/<Vendor>_<Module>`    Module specific layouts, styles, templates
3. `/<Vendor>_<Module>/web/css/source`  .css or .less files, styles for the module are in the _module.less file and for widgets are in _widgets.less
4. `/<Vendor>_<Module>/layout`    layout files which extend the default module or parent theme layouts
5. `/<Vendor>_<Module>/layout/override/base`    layouts which override the default module layouts
6. `/<Vendor>_<Module>/layout/override/<parent_theme>`   layouts that override the parent theme layouts
7. `/<Vendor>_<Module>/templates`   theme templates which override the default module templates, or parent theme templates. Also custom templates stored here
8. `/etc/view.xml`   image confirmation
9. `/i18n`  .csv files with translations
10. `/media`   Contains a theme preview file
11. `/web`   static files to be loaded from the frontend
12. `/web/css/source`   less conf files, and a theme.less file which overrides the default variable values
13. `/web/css/source/lib`   view files that override the UI library files in lib/web/css/source/lib
14. `/web/fonts`   theme fonts
15. `/web/images`   images used in the theme
16. `/web/js`   theme JS files
17. `/composer.json`   describes theme dependencies, mainly for themes that are composer packages
18. `/registration.php`   register your theme with the system
19. `/theme.xml`   declare theme, and basic meta

### 2.5 Theme file types
1. Static view files: Returned to the browser as is, with no processing. In `/media`, `/web/css`, `/web/fonts`, `/web/images`, `/web/js`. These files are published under `/pub/static/frontend/<Vendor>/<theme>/<language>/*`
2. Dynamic view files: Processed by the server, these are .less files, templates and layouts
