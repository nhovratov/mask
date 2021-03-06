﻿.. include:: ../Includes.txt

.. _upgrade:

=============
Upgrade Guide
=============

Mask tries to minimize breaking changes between each version. But sometimes small changes have to be done, which
require actions to be performed.

From v5 or lower
================

richtextConfiguration has to be removed
---------------------------------------

Because of a `changed loading order <https://docs.typo3.org/c/typo3/cms-core/master/en-us/Changelog/10.2/Important-88655-ChangedLoadingOrderOfRTEConfiguration.html>`__
of the RTE configuration it is required to remove the `richtextConfiguration` entry from `mask.json` or else all of your
RTE fields will have the TYPO3 default RTE config set.

.. versionadded:: 6.2.0

Mask provides the UpgradeWizard `RemoveRichtextConfiguration.php` to remove all entries at once.

.. important::
   This upgrade wizard is only available in Mask v6. The reason is that since v7 the richtext configuration can be
   edited in mask directly. If you are planning to update to v7, first update to v6, run the upgrade wizard and then
   continue updating to v7.

Command with TYPO3 CLI:

::

   ./typo3/sysext/core/bin/typo3 upgrade:run removeRichtextConfiguration

Or with typo3_console:

::

   ./typo3cms upgrade:run removeRichtextConfiguration

Another way is to go to the **Upgrade** module and open the **Upgrade Wizard**. There you will find `Remove "richtextConfiguration" in mask.json`.
Click on `Execute` to start the upgrade.

From v3 or lower
================

New template name format
------------------------

Since version v4 Mask is based on the FLUIDTEMPLATE content object. This requires all template files to be named
in UpperCamelCase.

Before: `my_element.html`

After: `MyElement.html`

.. versionadded:: 6.2.0

If you have a lot of templates you can rename them with the UpgradeWizard `ConvertTemplatesToUppercase.php`.

Command with TYPO3 CLI:

::

   ./typo3/sysext/core/bin/typo3 upgrade:run convertTemplatesToUppercase

Or with typo3_console:

::

   ./typo3cms upgrade:run convertTemplatesToUppercase

Another way is to go to the **Upgrade** module and open the **Upgrade Wizard**. There you will find `Convert Mask templates to uppercase.`.
Click on `Execute` to start the upgrade.

From 3.1.0 or lower
===================

New filename format for preview images
--------------------------------------

Remove the `ce_` prefix from all content element preview images. Example: from `ce_key.png` to `key.png`
