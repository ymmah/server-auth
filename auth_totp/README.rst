.. image:: https://img.shields.io/badge/license-LGPL--3-blue.png
   :target: https://www.gnu.org/licenses/lgpl.html
   :alt: License: LGPL-3

====================
MFA Support via TOTP
====================

This module adds support for MFA using TOTP (time-based, one-time passwords). 
It allows users to enable/disable MFA and manage authentication apps/devices 
via the "Change My Preferences" view and an associated wizard. 

After logging in normally, users with MFA enabled are taken to a second screen 
where they have to enter a password generated by one of their authentication 
apps and are presented with the option to remember the current device. This 
creates a secure, HTTP-only cookie that allows subsequent logins to bypass the 
MFA step.

Installation
============

1. Install the PyOTP library using pip: ``pip install pyotp``
2. Follow the standard module install process

Configuration
=============

By default, the trusted device cookies introduced by this module have a 
``Secure`` flag. This decreases the likelihood of cookie theft via
eavesdropping but may result in cookies not being set by certain browsers
unless your Odoo instance uses HTTPS. If necessary, you can disable this flag
by going to ``Settings > Parameters > System Parameters`` and changing the
``auth_totp.secure_cookie`` key to ``0``.

Usage
=====

If necessary, a user's trusted devices can be revoked by disabling and
re-enabling MFA for that user.

.. image:: https://odoo-community.org/website/image/ir.attachment/5784_f2813bd/datas
   :alt: Try me on Runbot
   :target: https://runbot.odoo-community.org/runbot/251/11.0

Known Issues / Roadmap
======================

Known Issues
------------

* External calls to the Odoo XML-RPC API are blocked for users who enable MFA
  since there is currently no way to perform MFA authentication as part of this
  process. However, due to the way that Odoo handles authentication caching,
  multi-threaded or multi-process servers will need to be restarted before the
  block can take effect for users who have just enabled MFA.

Roadmap
-------

* Make the lifetime of the trusted device cookie configurable rather than fixed
  at 30 days
* Add device fingerprinting to the trusted device cookie
* Add company-level settings for forcing all users to enable MFA and disabling 
  the trusted device option
* Monkey patch 1 is not needed anymore in Werkzeug==0.13 or upper
* Monkey patch 2 will work until werkzeug.contrib gets removed.

Bug Tracker
===========

Bugs are tracked on `GitHub Issues
<https://github.com/OCA/server-auth/issues>`_. In case of trouble, please
check there if your issue has already been reported. If you spotted it first,
help us smash it by providing detailed and welcomed feedback.

Credits
=======

Images
------

* Odoo Community Association: `Icon <https://odoo-community.org/logo.png>`_.

Contributors
------------

* Oleg Bulkin <obulkin@laslabs.com>

Do not contact contributors directly about support or help with technical issues.

Maintainer
----------

.. image:: https://odoo-community.org/logo.png
   :alt: Odoo Community Association
   :target: https://odoo-community.org

This module is maintained by the OCA.

OCA, or the Odoo Community Association, is a nonprofit organization whose
mission is to support the collaborative development of Odoo features and
promote its widespread use.

To contribute to this module, please visit https://odoo-community.org.
