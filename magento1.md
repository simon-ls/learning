# Magento 1

## 1. MVC
### MVC
* Configuration-based MVC system (not a convention-based system)
* In a configuration-based system you need to add the file AND explicitly tell the system about the new class.
* Each module has a file named config.xml, this contains all the relevant config for the module

* You'll find Controllers, Models, Helpers, Blocks, etc for Magneto's checkout in: app/code/core/Mange/Checkout
* Extend Magento by adding addition code in app/code/local/Packagename/Modulename

* Package name works like a Namespace, as may be referred to as this.
* When you create a new Module, you need to tell Magento about it, by adding an XML file to the folder.
* In this folder there are two kinds of file: (1) an individual Module, and is named in the form Packagename_Modulename.xml (2) a file that will enable multiple modules and named in the form Packagename_All.xml (this is only used by the core team, and should not be used normally, as it reduces modularity).

### MVC: Controllers
* Every URL is routed to a Controller, and then looks at an Action
* All Controllers in the Magento cart application extend from Mage_Core_Controller_Front_Action
* For example: http://example.com/catalog/category/view/id/25
    * `/catalog/`: front name, usually module name: `app/code/core/Mage/Catalog`
    * `/category/`: controller name: `app/code/core/Mage/Catalog/controllers/CategoryController.php`
    * `/view/`: action name, turned into viewAction()
    * `/id/25/`: any path portions after the action name, will be considered key/value GET request variables
* If the router cannot find an Controller/Action, it will look for an admin Controller/Action, if not, it will look in the CMS, if not it will return a 404
* Models, Helpers, and Blocks can be instantiated using:
```
Mage::getModel('catalog/product')
Mage_Catalog_Model_Product
Mage::helper('catalog/product')
Mage_Catalog_Helper_Product
```
* The string 'catalog/product' is a Grouped Class Name/URI. The first part is the Module and second is the Class.

### MVC: Models
* Magento uses Object Relational Mapping (ORM)
* Methods can be chained
* Items are then returned as PHP Objects

### MVC: Helpers
* Helper classes contain utility methods that will help perform common tasks
* Helpers usually inherit from Mage_Core_Helper_Abstract, which have useful methods

### MVC: Layouts (Views kinda of)
* A layout is an object that contains a nested/tree collection of "Block" elements. Each block will render a specific bit of HTML.
* Block classes are used to interact with Magneto to retrieve data, they also act as mini-controllers, and the .phtml files are the views to product HTML for a page
* In a Controller at least 2 functions will be called: $this->loadLayout() and $this->renderLayout()
* Magento will load up a Layout with a skeleton site structure, and will provide some Structure Blocks: html, head, body, columns, and Content Blocks for navigation, default welcome messages etc. A Block does not programmatically know if it's Structure of Content, but a Block is one or the other.
* To add Content to this Layout, you say "Magento, add these additional Blocks under the "content" Block of the skeleton", this can be done programmatically, but usually done using the XML Layout system.

### MVC: Layouts: XML Layouts
* Layout XML allows you to, on a per Controller bassis, remove or add Blocks to the default skeleton areas.
* Eg. In the Module: catalog, in Controller: category, in the Action: default, insert the catalog/navigation Block, into the "left" structure Block. Use the template catalog/navigation/left.phtml
```
<catalog_category_default>
     <reference name="left">
          <block type="catalog/navigation" name="catalog.leftnav" after="currency" template="catalog/navigation/left.phtml"/>
     </reference>
</catalog_category_default>
```
* In addition, you can use nested Blocks. Set this up by first including a nested Block in the Layout XML. Then you will be able to use $this->getChildHtml('order_items'), if you do not include in your XML, it will render blank
```
...
<block type="catalog/navigation" name="catalog.leftnav" after="currency" template="catalog/navigation/left.phtml">
     <block type="core/template" name="foobar" template="foo/baz/bar.phtml"/>
</block>
...
```

### Etc: Observers
* Users can hook into Event/Object pattern. Events are triggered as actions happen, when creating a Module, you can listen for these events.
* You can set these up in config.xml. This is an example, it will call Packagename_Mymodule_Model_Observer::iSpyWithMyLittleEye
```
<events>
     <customer_login>
          <observers>
               <unique_name>
                    <type>singleton</type>
                    <class>mymodule/observer</class>
                    <method>iSpyWithMyLittleEye</method>
               </unique_name>
          </observers>
     </customer_login>
</events>
```

### Etc: Class Overrides
* You can replace Model, Helper and Block classes from the core modules, with your own.
* This is done in the config.xml file, and will call the new method instead of the old:
```
<models>
    <!-- does the override for catalog/product-->
    <catalog>
        <rewrite>
            <product>Packagename_Modulename_Model_Foobazproduct</product>
        </rewrite>
    </catalog>
</models>
```

## 2. Theming

Folder structure
```
app/
     code/
          {core,local,community}/
               Company/
                    Module/
                         Block/ (Block classes)
```
```
app/
     design/
          frontend/
               base/
                    default/
                         layout/
                         template/
               mytheme/
                    default/
                         layout/ (xml)
                         template/ (phtml)
                    christmas/
                         layout/
                         template/
```
```
skin/
     frontend/
          base/
               default/
                    css/
                    images/
          mytheme/
                    default/
                         css/
                         images/
                    christmas/
                         css/
                         images/
```

* View of MVC are Layouts

### MVC Steps
1. Action Controller will then instantiate a Layout Object
2. This Layout Object will, based on request variables and system properties, create a list of Block objects
3. Layouts will call an output method on some Block objects, which start a nested rendering (Blocks inside of Blocks)
4. Each Block has a template file
5. Blocks refer directly back to the models for their data (the Action Controller does not pass them data).

### Templating
1. Magento MVC Controllers do not pass a data object to the view, or set properties on the view object
2. The View directly references system models to get the information it needs for display

#### Templating: XML Layout Files
* XML Layout is a collection of `<block>`s (and other elements). Magento will go through this and find a Block class and .phtml file for each `<block>`
* `<block>`s can be nested again and again.
* type="" is the Block class URI
* If there are two blocks with the same name, the new block will replace the old
* The Handle is created by combining the route name (helloworld), Action Controller name (index), and Action Controller Action Method (index)
* local.xml is the last file merged in, and where you can add your customizations to Magneto install, it is often best to put your changes in this file (in your own interface/theme)

#### Templating: Blocks classes
* Debug with: print_r($this->getLayout()->getUpdate()->getHandles());
* Various helper methods, like getSkinUrl('path') or getUrl('path') are contained in all block classes
* getChildHtml() allows you to call nested blocks in a layout. But these must be defined first in Layout XML
* Usually toHtml() is called, and the phtml file is pharsed, but this could be changed (i.e to return JSON)

#### Templating: Template Files (phtml)
* getChildHtml() is used to render another block
* Each template file is connected to a Block via $this


### XML Layout: Block
* `<block>`
* type="" Defines the functionality of the block, and links to Block class. Can find out classname with get_class($this);
* name="" By which other blocks can identify, always unique
* before="", after="" Position a block in a structural block
* template="" PHTML template
* as="" Alias by which the parent block refer to a child block, by default the alias is equal to the name.

### XML Layout: References
* `<reference name="" />` will hook all contained XML declarations into an existing block, with the specific name (`<block type="..." name="" />`)
* Contained blocks, will be assigned as children of referenced parent block

### XML Layout: Update
* The  `<update handle="" />` tag allows you to include the `<blocks>`s from another Handle's tag

### XML Layout: Remove
* `<remove name="" />`

### XML Layout: Update
* `<action method="" />` allows us to call public PHP methods of the Block class.
* All arguments to the action's method need to be wrapped in an individual child node of the `<action>`, the name of the node does not matter, only the order of the notes


### Block Types
1. core/template: This block renders a template defined by its template attribute. The majority of blocks defined in the layout are of type or subtype of core/template. Mage_Core_Block_Template
2. page/html: This is a subtype of core/template and defines the root block. All other blocks are child blocks of this block.
3. page/html_head: Defines the HTML head section of the page which contains elements for including JavaScript, CSS etc.
4. page/html_header: Defines the header part of the page which contains the site logo, top links, etc.
5. page/template_links: This block is used to create a list of links. Links visible in the footer and header area use this block type.
6. core/text_list: Some blocks like content, left, right etc. are of type core/text_list. When these blocks are rendered, all their child blocks are rendered automatically without the need to call thegetChildHtml() method. Mage_Core_Block_Text_List
7. page/html_wrapper: This block is used to create a wrapper block which renders its child blocks inside an HTML tag set by the action setHtmlTagName. The default tag is `<div>` if no element is set. Mage_Page_Block_Html_Wrapper
8. page/html_breadcrumbs: This block defines breadcrumbs on the page.
9. page/html_footer: Defines footer area of page which contains footer links, copyright message etc.
10. core/messages: This block renders error/success/notice messages.
11. page/switch: This block can be used for the language or store switcher.


## Good Practice:
when testing for a yes/no value in magento attribute do not use getAttributeText use getData

## URLS

### Get Base Url
```
Mage::getBaseUrl();
```
### Get Skin Url :
```
Mage::getBaseUrl(Mage_Core_Model_Store::URL_TYPE_SKIN);
```
#### (a) Unsecure Skin Url :
```
$this->getSkinUrl('images/imagename.jpg');
```
#### (b) Secure Skin Url :
```
$this->getSkinUrl('images/imagename.gif', array('_secure'=>true));
```
### Get Media Url :
```
Mage::getBaseUrl(Mage_Core_Model_Store::URL_TYPE_MEDIA);
```
### Get Js Url :
```
Mage::getBaseUrl(Mage_Core_Model_Store::URL_TYPE_JS);
```
### Get Store Url :
```
Mage::getBaseUrl(Mage_Core_Model_Store::URL_TYPE_WEB);
```
### Get Current Url
```
Mage::helper('core/url')->getCurrentUrl();
```
Get Url in cms pages or static blocks

### Get Base Url :
```
{{store url=""}}
```
### Get Skin Url :
```
{{skin url='images/imagename.jpg'}}
```
### Get Media Url :
```
{{media url='/imagename.jpg'}}
```
### Get Store Url :
```
{{store url='mypage.html'}}
```
