# Scripts

Scripts allow you to writing PHP code in order to used as a controller but in this case it can return what it wants.

The aim of the scripts is not pollute views in providing the capability to get "_**Params**_'', "_**Response**_", "_**Request**_" et use "_**Plugins**_".

##Plugins

So you can use Zend controller plugins:

*   [_AcceptableViewModelSelector_](http://framework.zend.com/manual/2.1/en/modules/zend.mvc.plugins.html#zend-mvc-controller-plugins-acceptableviewmodelselector)
*   [_FlashMessenger_](http://framework.zend.com/manual/2.2/en/modules/zend.mvc.plugins.html#zend-mvc-controller-plugins-flashmessenger)
*   [_Forward_](http://framework.zend.com/manual/2.2/en/modules/zend.mvc.plugins.html#zend-mvc-controller-plugins-forward)
*   [_Identity_](http://framework.zend.com/manual/2.2/en/modules/zend.mvc.plugins.html#zend-mvc-controller-plugins-identity)
*   [_Layout_](http://framework.zend.com/manual/2.2/en/modules/zend.mvc.plugins.html#zend-mvc-controller-plugins-layout)
*   [_Params_](http://framework.zend.com/manual/2.2/en/modules/zend.mvc.plugins.html#zend-mvc-controller-plugins-params)
*   [_PostRedirectGet_](http://framework.zend.com/manual/2.2/en/modules/zend.mvc.plugins.html#zend-mvc-controller-plugins-postredirectget)
*   [_Redirect_](http://framework.zend.com/manual/2.2/en/modules/zend.mvc.plugins.html#zend-mvc-controller-plugins-redirect)
*   [_Url_](http://framework.zend.com/manual/2.2/en/modules/zend.mvc.plugins.html#zend-mvc-controller-plugins-url)

##Request, Response and Service Manager

Method "**getRequest**" return an instance of **Zend\Http\PhpEnvironment\Request**.

"**getResponse**" an instance of **Zend\Http\PhpEnvironment\Response**.

**"getServiceLocator"** an instance of **Zend\ServiceManager\ServiceManager**.

&nbsp;

##Params

If you need, you can pass parameters to script.

In your view:

```php
$return = $this->script('myScript', array('myParam' => true));
```

In your script

```php
$this->getParam('myParam');
```


##Example

```php
$request = $this->getRequest();
if ($request->isPost()) {
    $post = $request->getPost();
    $name = $post->get('name');
    $email = $post->get('email');
    $message = $post->get('message');
    $answerHash = $post->get('answer_hash');
    $answer = substr(sha1($post->get('answer')), 5, 10);
 
    if ($answer != $answerHash or empty($name) or empty($email) or empty($message)) {
        return array('name' => $name, 'email' => $email, 'message' => $message, 'error_message' => 'Please fill all fields');
    } else {
        $mail = new \Gc\Mail('utf-8', $message);
        $mail->setFrom($email, $name);
        $mail->addTo($this->getServiceLocator()->get('CoreConfig')->getValue('mail_from'));
        $mail->send();
        $this->flashMessenger()->setNameSpace('success')->addMessage('Message sent');
        $this->redirect()->toUrl('/contact');
        return true;
    }
}
```
