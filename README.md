## How to control the loading of module positions based on the active component

Add the following line to the PHP block at the beginning of your template's index.php:  
```php
$whatComp = JFactory::getApplication()->input->get('option');
```

You need to know the system name of your component. For example, K2 is named **com_k2**.

Now around a module position code loader (you know, the <jdoc:include... thing) you should add a PHP if statement, like this:

```php
<?php if($whatComp == "com_whatever") { ?>
  <?php if ($this->countModules('here-goes-a-module')): ?>
    <div id="my-wonder-module">
      <jdoc:include type="modules" name="here-goes-a-module" style="standard" />
    </div>
  <?php endif; ?>
<?php } ?>
```

### How to further refine the module loading based on a specific view/layout

Add the following lines below the $whatComp line:  
```php
$whatView = JFactory::getApplication()->input->get('view');
$whatLayout = JFactory::getApplication()->input->get('layout');
```

With this you'll be able to narrow down the module position even more.

## How is that useful?

* Module loading isn't really fine tuned in Joomla
* We don't want to resort to the overly complicated RegularLabs Advanced Module Manager
* Your client isn't really knowledgeable with Joomla, and you want to provide an easy-to-use solution
