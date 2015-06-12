# Datatypes

Datatype or simply type is a classification identifying one of various types of data, such as text field, integer, boolean or file upload, that determines the possible values for that type.

In this case, Datatype needs three classes to works:

* Datatype as Bootstrap
* PrevalueEditor as Configuration
* Editor as Content part

Replace all texts in this **<span style="color:#FF9900;">color</span>** with the name you want to use for your datatype and classes must be added in "library/Datatypes/**<span style="color:#FF9900;">DatatypeName</span>**" directory.

##Bootstrap

```php
namespace Datatypes\DatatypeName;
     
use Gc\Datatype\AbstractDatatype as AbstractDatatype;
use Gc\Property\Model as PropertyModel;
     
class Datatype extends AbstractDatatype
{
    /**
     * Datatype name
     *
     * @var string
     */
    protected $name = 'datatype-name';
     
     /**
      * Retrieve editor
      *
      * @param PropertyModel $property Property
      *
      * @return \Gc\Datatype\AbstractDatatype\AbstractEditor
      */
    public function getEditor(PropertyModel $property)
    {
        $this->setProperty($property);
        if ($this->editor === null) {
            $this->editor = new Editor($this);
        }
 
        return $this->editor;
    }
 
    /**
     * Retrieve prevalue editor
     *
     * @return \Gc\Datatype\AbstractDatatype\AbstractPrevalueEditor
     */
    public function getPrevalueEditor()
    {
        if ($this->prevalueEditor === null) {
            $this->prevalueEditor = new PrevalueEditor($this);
        }
 
        return $this->prevalueEditor;
    }
}
```

##Prevalue Editor
```php
namespace Datatypes\DatatypeName;
 
use Gc\Datatype\AbstractDatatype\AbstractPrevalueEditor;
use Zend\Form\Element;
 
class PrevalueEditor extends AbstractPrevalueEditor
{
    /**
    * Save prevalue editor
    *
    * @return void
    */
    public function save()
    {
        $this->setConfig(/*string, array, objects, etc...*/);
    }
 
    /**
    * Load textstring prevalue editor
    *
    * @return mixed
    */
    public function load()
    {
        return; //objects, array, strings, Zend\Form\Element
    }
}
```
##Editor
```php
namespace Datatypes\DatatypeName;
 
use Gc\Datatype\AbstractDatatype\AbstractEditor;
use Zend\Form\Element;
 
class Editor extends AbstractEditor
{
    /**
    * Save textstring editor
    *
    * @return void
    */
    public function save()
    {
        $this->setValue('//string (serialize or not)');
    }
 
    /**
    * Load textstring editor
    *
    * @return mixed
    */
    public function load()
    {
        //return objects, array, strings, Zend\Form\Element
    }
}
```

##Informations file

You also can add an datatype.ini file to specify:

*   version (string)
*   author (string)
*   date (string)
*   description (string)
*   cms_version (string)
*   website (link)
*   database_compatibility (array)
