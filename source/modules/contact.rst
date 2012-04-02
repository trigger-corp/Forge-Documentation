.. _modules-contact:

``contact``: Accessing contacts
================================================================================

**Platforms: Mobile**

The ``forge.contact`` namespace allows access to the native contact address book on the device the app is running on.

Contacts are represented by a simple Javascript object which follows the `W3C Contacts API <http://www.w3.org/TR/contacts-api/#contact-interface>`_ as much as possible.

Config
------

The ``contact`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "contact": true
        }
    }

API
---

``select``
~~~~~~~~~~
**Platforms: Mobile**

Prompts the user to select a contact and returns a contact object.

.. js:function:: contact.select(success, error)

    :param function(contact) success: callback to be invoked when no errors occur
    :param function(content) error: called with details of any error which may occur


Contact object
--------------

Below is an example of a returned contact object, with details for some field types.

.. parsed-literal::

    {
      ":ref:`id <field-contact-id>`": "14894",
      ":ref:`displayName <field-contact-displayName>`": "Mr Joe Bloggs",
      ":ref:`name <field-contact-name>`": {
        "formatted": "Mr Joe Bloggs",
        "familyName": "Bloggs",
        "givenName": "Joe",
        "middleName": null,
        "honorificPrefix": "Mr",
        "honorificSuffic": null
      },
      ":ref:`nickname <field-contact-nickname>`": "Joe",
      ":ref:`phoneNumbers <field-contact-phoneNumbers>`": [
        {
          "value": "+447554639203",
          "type": "work",
          "pref": false
        }
      ],
      ":ref:`emails <field-contact-emails>`": [
        {
          "value": "joe-bloggs@trigger.io",
          "type": "work",
          "pref": false
        }
      ],
      ":ref:`addresses <field-contact-addresses>`": [
        {
          "country": "United Kingdom",
          "formatted": "1-11 Baches Street\\nLondon\\nLondon\\N1 6DL\\nUnited Kingdom",
          "locality": "London",
          "postalCode": "N1 6DL",
          "pref": false,
          "region": "London",
          "streetAddress": "1-11 Baches Street",
          "type": "work"
        }
      ],
      ":ref:`ims <field-contact-ims>`": [
        {
          "value": "joe-bloggs@trigger.io",
          "type": "gtalk",
          "pref": false
        }
      ],
      ":ref:`organizations <field-contact-organizations>`": [
        {
          "department": "Product development",
          "name": "Forger",
          "pref": false,
          "title": "Software engineer",
          "type": null     
        }          
      ],
      ":ref:`birthday <field-contact-birthday>`": "1983-11-23",
      ":ref:`note <field-contact-note>`": "Any text can go here",
      ":ref:`photos <field-contact-photos>`": [
        {
          "value": "data:image/jpg;base64,ABCDEF1234",
          "type": null,
          "pref": false
        }
      ],
      ":ref:`categories <field-contact-categories>`": null,
      ":ref:`urls <field-contact-urls>`": [
        {
          "value": "http://trigger.io",
          "type": "homepage",
          "pref": false
        }
      ],
    }
    
Fields
~~~~~~

This section includes more detailed information on the contents of fields with non-obvious content.

.. _field-contact-id:

id
'''''''''''''

This is a unique identifier for the contact, and is guaranteed to be the same if the user selects the same contact again.

.. _field-contact-displayName:

displayName
'''''''''''''

This is a formatted version of the contacts name which can be used for display. On iOS this is generated from the various parts of the name, on Android this is stored as a separate value.

.. _field-contact-name:

name
'''''''''''''

This is an object containing the various parts of the contacts name, including a formatted version which is used as the previous displayName value.

.. _field-contact-nickname:

nickname
'''''''''''''

A string value containing a nickname for the contact

.. _field-contact-phoneNumbers:

phoneNumbers
'''''''''''''

An array of objects containing details of a contacts phone numbers. Each number has a ``value``, a ``type`` (such as ``home`` or ``work``) and also a ``pref`` property, which is unsupport on Android and iOS so is always false.

.. _field-contact-emails:

emails
'''''''''''''

Similarly this property is an array of objects describing a contacts emails, with ``value``, ``type`` and ``pref`` (which is also always false).

.. _field-contact-addresses:

addresses
'''''''''''''

An array of objects describing a contacts addresses, ``formatted`` contains a string generated from the other properties which can be used to display the address. Each object also contains a ``pref`` property which is always false.

.. _field-contact-ims:

ims
'''''''''''''

Contains an array of Instant Messaging details for a contact, formatted similarly to phoneNumbers and emails.

.. _field-contact-organizations:

organizations
'''''''''''''

Contains an array of objects describing organizations the contact is part of.

Can only contain one organization on iOS.

.. _field-contact-birthday:

birthday
'''''''''''''

Contains a string with the date of birth of the contact.

.. _field-contact-note:

note
'''''''''''''

A string which can contain arbitrary information about the contact.

.. _field-contact-photos:

photos
'''''''''''''

Contains an array of thumbnail photos associated with the contact, each photo has a value which contains a ``data:`` uri of the image. The ``type`` and ``pref`` properties are not used.

Contains at most 1 photo on iOS.

.. _field-contact-categories:

categories
'''''''''''''

Not available on iOS or Android.

.. _field-contact-urls:

urls
'''''''''''''

Contains an array of URLs related to the contact, formatted similarly to phoneNumbers and emails.

Permissions
-----------

On Android this module will add the ``READ_CONTACTS`` permission to your app, users will be prompted to accept this when they install your app.
