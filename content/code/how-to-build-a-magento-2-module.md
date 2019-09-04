---
title: "How to Build a Magento 2 Module"
date: 2019-09-03T10:54:12+02:00
draft: true
tags: ["Magento"] 
---

# Basics

```
cd app/code
mkdir -p Vendorname/Modulename/etc
cd Vendorname/Modulename
touch etc/module.xml
touch registration.php
```

Copy this to etc/module.xml:
```
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
	<module name="Learning_FirstUnit" setup_version="0.0.1">
		<sequence>
			<module name="Magento_Catalog"/>
		</sequence>
    </module>
</config>
```

The first module node defines the name and version of your module.
Version triggers update command, if the deployed version is older than the updatet version.
The second module node specifies which existing module your module depends on.
One module node for every module you need as a dependency.


Copy this to registration.php:
```
<?php \Magento\Framework\Component\ComponentRegistrar::register(
	\Magento\Framework\Component\ComponentRegistrar::MODULE, 'Learning_FirstUnit',
	__DIR__
);
```

This tells Magento where your module can be found. It reflects the directory structure of app/code/Vendorname/Modulename

These steps are the same for every module you create. The only differences will be module names, versions and dependencies.

You can already activate your module at this point:
```
php bin/magento setup:upgrade
```

Verify it's there:
```
grep Vendorname_Modulename app/etc/config.php
```

# Creating a Page


