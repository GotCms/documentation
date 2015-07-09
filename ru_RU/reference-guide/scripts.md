# Scripts

Скрипты (Scripts) позволяют вам писать PHP код для использования его как контроллера но в этом случае он просто возвращает значения в вид.

Цель скриптов не допускать засорения кода видов при использовании возможностей "_**Params**_'', "_**Response**_", "_**Request**_"  и использования "_**Plugins**_".

##Plugins

Вы можете использовать стандартные плагины контроллеров Zend:

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

Метод "**getRequest**" возвращает экземпляр класса **Zend\Http\PhpEnvironment\Request**.

"**getResponse**"  - экземпляр класса **Zend\Http\PhpEnvironment\Response**.

**"getServiceLocator"** - экземпляр класса **Zend\ServiceManager\ServiceManager**.

&nbsp;

##Params

Если вам необходимы, то вы можете передавать параметры в скрипт из вида.

Для этого в виде задаете:

```php
$return = $this->script('myScript', array('myParam' => true));
```

а в скрпите используете

```php
$this->getParam('myParam');
```


##Пример

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
