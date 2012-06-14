.. _tools-ios-windows:

Developing iOS apps on Windows and Linux
================================================================================

Forge allows the development of iOS apps on Windows and Linux without the use
of an OS X machine. To do this you will need a physical iOS device (the iOS
simulator will only run on OS X), and an iOS developer account. In order
to sign your application (which is required to install it onto the device, even
for testing), we provide a remote signing service, which your app will be sent
to, signed and returned as part of the ``forge run`` and ``forge package``
command.

Setting up Forge to run iOS apps
--------------------------------

Requirements:

- Apple iOS developer account.
- iTunes or iPhone Configuration Utility installed on the machine you are going to develop on
- An iOS device connected via USB to the machine you wish to develop on

In order to sign your application you need to provide us with the following:

- A signing certificate and password
- A provisioning profile

Both of these can be created and managed from the Apple iOS provisioning
portal, which should be accessible from the iOS developer center:
https://developer.apple.com/ios/. The instructions on that site are for OS X,
more detailed instructions for creating a developer certificate on Windows are
included below.

Once these are setup you should be able to use ``forge run ios`` to install the app on your device and see log output in the terminal on your computer.

Creating a signing certificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a certificate you need to generate a certificate signing request, in
Windows this can be done by following these steps:

- Create a file ``request.txt`` with the following content, replacing ``Connor
  Dunn`` with the name registered to your Apple Developer account::

    [NewRequest]
    Subject="cn=Connor Dunn,o=User"
    RequestType=pkcs10
    KeyLength=2048
    Exportable=TRUE

- Run the following command in the same directory as ``request.txt``: ``certreq -new request.txt``
- On the iOS provisioning portal site choose to create a new certificate and upload the file you just created
- Your certificate request should be approved shortly: when it is, download and open the certificate file. Windows should prompt you to install the certificate.
- Once installed, run the command ``certmgr.msc``: this should open a certificate management tool. In this tool browse to ``Personal`` certificates, you should see the iPhone Developer certificate you just installed.
- You should be able to right click on the certificate and choose All tasks -> Export. Make sure you export the private key as part of the certificate when following the wizard. The password you supply will be the one you need to provide to Forge, and prevents unauthorized users from using the certificate if they were to come into possession of the certificate file.
- You should now be able to configure the ``developer_certificate_path`` and ``developer_certificate_password`` in your ``local_config.json`` file.

.. note:: See :ref:`parameters-in-a-file` for more information on your ``local_config.json`` file.

Creating a provisioning profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once you have created a certificate you need to create a provisioning profile, this is also done via the iOS provisioning portal website:

- First make sure your device has been added to the provisioning portal, to do this you will need the device identifier (UDID), this can be found by clicking on the device's serial number in iTunes.
- Next create an app id, for development entering ``*`` as a Bundle Identifier is recommended, as it means multiple apps can be signed with a single provisioning profile.
- Finally create a development provisioning profile, making sure you choose the correct app id and enable any devices you wish to be able to test with.
- You can now download and configure the location of your provisioning profile in ``local_config.json``.

.. note:: Provisioning profiles must be recreated if certificates or devices are changed.
