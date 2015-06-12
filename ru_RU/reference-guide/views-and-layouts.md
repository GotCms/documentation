# Views and layouts

_Note: pieces of texts come directly from the official documentation of Zend Framework ([http://framework.zend.com/manual/2.2/en/modules/zend.view.php-renderer.scripts.html](http://framework.zend.com/manual/2.2/en/modules/zend.view.php-renderer.scripts.html))_

Once your document has assigned variables via identifier or you call view via a partial helper, you might want to display some values &#8203;&#8203;or some recurrent codes.

Firstly inside views and layouts<span>, the variable **$this** is an instance of Zend\View\Renderer\PhpRenderer<span>.

There are three ways to retrieve variables

* Explicitly, by retrieving them from the Variables container composed in the PhpRenderer: **`$this->vars()->varname**.
* As instance properties of the PhpRenderer instance: **`$this->varname**. (In this situation, instance property access is simply proxying to the composed Variables instance.)
* As local PHP variables: **$varname**. The PhpRenderer extracts the members of the Variables container locally.

We generally recommend using the second notation, as it’s less verbose than the first, but differentiates between variables in the view script scope and those assigned to the renderer from elsewhere.

Here is the example view script from the PhpRenderer introduction:

```
<div>
    <?php echo $this->partial('sidebar'); ?>
    <div>
        <section>
            <h1><?php echo $this->escapeHtml($this->translate($this->pageTitle)); ?></h1>
            <?php echo $this->pageContent; ?>
        </section>
    </div>
 
    <?php if($this->contacts): ?>
        <div>
            <?php foreach($this->contacts as $contact): ?>
                <p><?php echo $this->escapeHtml($contact); ?></p>
            <?php endforeach; ?>
        </div>
    <?php endif; ?>
</div>
```

## Dealing with layouts

Most sites enforce a cohesive look-and-feel which we typically call the site’s “layout”. It includes the default stylesheets and JavaScript necessary, if any, as well as the basic markup structure into which all site content will be injected. All specification defined for views are also defined in layout. To include view in layout, view will capture to the "content" variable of the layout.

This means you can do the following in your layout script:

```
<html>
    <head>
        <title><?php echo $this->escapeHtml($this->title); ?></title>
    </head>
    <body>
        <?php echo $this->content; ?>
    </body>
</html>
```

## Helpers

In your view scripts, often it is necessary to perform certain complex functions over and over: e.g., formatting a date, generating form elements, or displaying action links. You can use helper, or plugin, classes to perform these behaviors for you.

As you can see, three helpers are called in this view:

* **partial**: used to render a specified template within its own variable scope
* **escapeHtml**: escape Html text
* **translate**: translate string

All Zend Framework functions related to Zend\View\PhpRenderer can be used, that's includes:

* [View helpers](http://framework.zend.com/manual/2.2/en/modules/zend.view.helpers.html)
* [Form helpers](http://framework.zend.com/manual/2.2/en/modules/zend.form.view.helpers.html)
* [I18n helpers](http://framework.zend.com/manual/2.2/en/modules/zend.i18n.view.helpers.html)
* [Navigation helpers](http://framework.zend.com/manual/2.2/en/modules/zend.navigation.view.helpers.html)

GotCms add some helpers:

* **Acl:** Check admin user acl and return boolean
* **Admin:** Return current admin session
* **Cdn:** Add specific configured in backend before link for frontend (i.e: `$this->cdn('/frontend/images/my-project.png');`)
* **CdnBackend:** Add specific configured in backend before link for backend (i.e: `$this->cdn('/frontend/images/my-project.png');`)
* **Config:** Can retrieve or set some informations sotred in core_config_data table (i.e: `$this->config()->get('debug_is_active');`)
* **CurrentDocument****:** Return the current document
* **Document:** Retrieve document from id or url key (i.e: `$this->document('home');`)
* **Documents:** If parameter is empty return all root documents, if is numeric or string return all children, if is array return all document from url key or id (i.e: `$this->documents();` `$this->documents(1);` `$this->documents('home');` `$this->documents(array(1, 2, 'home'));`)
* **ModulePlugin:** Execute plugin module (i.e: `$this->modulePlugin('blog', 'commit-list');`
* **Script:** Execute script (i.e: `$this->script('identifier');`)
* **Tools:** Execute some php functions like serialize, unserialize, debug (i.e: `$this->tools('serialize', array('test'));`)

And overwrite:

* **Partial**: to include view from identifier
* **FormCheckbox**: for backend usage and design checkbox
* **FormMultiCheckbox**: same as FormCheckbox
