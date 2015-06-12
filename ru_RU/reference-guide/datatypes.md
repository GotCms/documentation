# Типы данных (Datatypes)

Тип данных или просто тип это классификационный идентификатор одного из различных типов вводимой информации, таких как "текстове поле" (text field), целое число (integer), булево значение (boolean) или имя файла для загрузки на сервер (file upload), который опреедляет допустимые значения для этого типа. ОДно из начначений типов данных - задавать валидаторы для поле, добавляемых в формы интерфейса.

Класс "Тип данных" (Datatype) требует наличия следующих трех классов:

* Datatype as Bootstrap
* PrevalueEditor as Configuration
* Editor as Content part

Replace all texts in this **<span style="color:#FF9900;">color</span>** with the name you want to use for your datatype and classes must be added in "library/Datatypes/**<span style="color:#FF9900;">DatatypeName</span>**" directory. (I think it will be good to explain where is this code placed. More information required.).

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

##Информационный файл (Informations file)

Вы так же можете добавить datatype.ini файл для определения:

*   версии - version (string)
*   автора - author (string)
*   даты - date (string)
*   краткого описания типа данных - description (string)
*   версии CMS - cms_version (string)
*   ссылки на сайт автора - website (link)
*   данных о совместимости баз данных - database_compatibility (array)
