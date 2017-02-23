## Get Base Url
```
Mage::getBaseUrl();
```
## Get Skin Url :
```
Mage::getBaseUrl(Mage_Core_Model_Store::URL_TYPE_SKIN);
```
### (a) Unsecure Skin Url :
```
$this->getSkinUrl('images/imagename.jpg');
```
### (b) Secure Skin Url :
```
$this->getSkinUrl('images/imagename.gif', array('_secure'=>true));
```
## Get Media Url :
```
Mage::getBaseUrl(Mage_Core_Model_Store::URL_TYPE_MEDIA);
```
## Get Js Url :
```
Mage::getBaseUrl(Mage_Core_Model_Store::URL_TYPE_JS);
```
## Get Store Url :
```
Mage::getBaseUrl(Mage_Core_Model_Store::URL_TYPE_WEB);
```
## Get Current Url
```
Mage::helper('core/url')->getCurrentUrl();
```
Get Url in cms pages or static blocks

## Get Base Url :
```
{{store url=""}}
```
## Get Skin Url :
```
{{skin url='images/imagename.jpg'}}
```
## Get Media Url :
```
{{media url='/imagename.jpg'}}
```
## Get Store Url :
```
{{store url='mypage.html'}}
```
