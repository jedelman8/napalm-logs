.. _configuration-options:

=====================
Configuration Options
=====================

Here we will list all options and what they do.

Command Line
++++++++++++

All of the command line arguments can also be added to a config file.

.. _configuration-options-address:

``address``
-----------

The IP address to use to listen for all incoming syslog messages.

Default: ``0.0.0.0``.

CLI usage example:

.. code-block:: bash

  $ napalm-logs -a 172.17.17.1
  $ napalm-logs --address 172.17.17.1

Configuration file example:

.. code-block:: yaml

  address: 172.17.17.1

.. _configuration-options-auth-address:

``auth-address``
----------------

The IP address to listen on for incoming authorisation requests.

Default: ``0.0.0.0``.

CLI usage example:

.. code-block:: bash

  $ napalm-logs --auth-address 172.17.17.2

Configuration file example:

.. code-block:: yaml

  auth_address: 172.17.17.2

.. _configuration-options-auth-port:

``auth-port``
-------------

The port to listen on for incoming authorisation requests.

Default: ``49018``

CLI usgae example:

.. code-block:: bash

  $ napalm-logs --auth-port 2022

Configuration file example:

.. code-block:: yaml

  auth_port: 2022

.. _configuration-options-certificate:

``certificate``
---------------

The certificate to use for the authorisation process. This will be presented to
incoming clients during the TLS handshake.

CLI usage example:

.. code-block:: bash

  $ napalm-logs --certificate /var/cache/server.crt

Configuration file example:

.. code-block:: yaml

  certificate: /var/cache/server.crt

.. _configuration-options-config-file:

``config-file``
---------------

Specifies the file where further configuration options can be found.

Default: ``/etc/napalm/logs``.

CLI usage example:

.. code-block:: bash

  $ napalm-logs -c /srv/napalm-logs
  $ napalm-logs --config-file /srv/napalm-logs

.. _configuration-options-config-path:

``config-path``
---------------

The directory path where device configuration files can be found. These are the
files that contain the syslog message format for each device.

CLI usage example:

.. code-block:: bash

  $ napalm-logs --config-path /home/admin/napalm-logs/

Configuration file example:

.. code-block:: yaml

  config_path: /home/admin/napalm-logs/

.. _configuration-options-device-worker-processes:

``device-worker-processes``: ``1``
----------------------------------

.. versionadded:: 0.3.0

This option configures the number of worker processes to be started for each
platform class. For better performances and higher capacity, it is recommended
to increase this number, which defaults to 1, i.e., by default there will be
started a single process per platform.

.. note::

    Increasing the number of processes, will imply higher memory consumption.

    For fine-tunning, consider increasing this number, and at the same time
    exclude (or include) the appropriate platforms, using the following options:
    :ref:`configuration-options-device-blacklist` and
    :ref:`configuration-options-device-whitelist`.

.. _configuration-options-disable-security:

``disable-security``
--------------------

If set no encryption or message signing will take place. All messages will be in
plain text. The client will not be able to verify that a message was generated
by the server.

**It is not recommended to use this in a production environment.**

CLI usage example:

.. code-block:: bash

  $ napalm-logs --disable-security

Configuration file example:

.. code-block:: yaml

  disable_security: true

.. _configuration-options-extension-config-path:

``extension-config-path``
-------------------------

A path where you can specify further device configuration files that contain the
syslog message format for devices.

CLI usage example:

.. code-block:: bash

  $ napalm-logs --extension-config-path /home/admin/napalm-logs/

Configuration file example:

.. code-block:: yaml

  extension_config_path: /home/admin/napalm-logs/

.. _configuration-hwm:

``hwm``: 1000
-------------

.. versionadded:: 0.3.0

This option controls the ZeroMQ high water mark (the hard limit on the maximum
number of outstanding messages ZeromMQ shall queue in memory).
If this limit has been reached the internal sockets enter an exceptional state,
and ZeroMQ blocks the reception of further messages.
This option can be used to tune the performances of the napalm-logs, in terms of
total messages processed. While the default limit should be generally
enough, in environments with extremely high density of syslog messages to be
processed, it is recommended to increase this value. Keep in mind that a higher
queue implies higher memory consumption.
For maximum capacity, this option can be set to ``0``, i.e., inifinite queue.

CLI usage example:

.. code-block:: bash

  $ napalm-logs --hwm 0

Configuration file example:

.. code-block:: yaml

  hwm: 0

.. _configuration-options-keyfile:

``keyfile``
-----------

The private key for the certificate specified by the ``certificate`` option.
This will be used to generate a key to encrypt messages.

CLI usage example:

.. code-block:: bash

  $ napalm-logs --keyfile /var/cache/server.key

Configuration file example:

.. code-block:: yaml

  keyfile: /var/cache/server.key

.. _configuration-options-listener:

``listener``
------------

The module to use when listening for incoming syslog messages. For more details,
see :ref:`listener`.

Default: ``udp``.

CLI usage example:

.. code-block:: bash

  $ napalm-logs --listener kafka

Configuration file example:

.. code-block:: yaml

  listener: kafka

.. _configuration-options-log-file:

``log-file``
------------

The file where to send log messages.

If you want log messages to be outputted to the command line you can specify
``--log-file cli``.

Default: ``/var/log/napalm/logs``.

CLI usage example:

.. code-block:: bash

  $ napalm-logs --log-file /var/log/napalm-logs

Configuration file example:

.. code-block:: yaml

  log_file: /var/log/napalm-logs

.. _configuration-options-log-format:

``log-format``
--------------

The format of the log messages.

Default: ``%(asctime)s,%(msecs)03.0f [%(name)-17s][%(levelname)-8s] %(message)s``.

Example: ``2017-07-03 11:54:25,300,301 [napalm_logs.listener.tcp][INFO    ] Stopping listener process``

CLI usage example:

.. code-block:: bash

  $ napalm-logs --log-format '%(asctime)s,%(msecs)03.0f [%(levelname)] %(message)s'

Configuration file example:

.. code-block:: yaml

  log_format: '%(asctime)s,%(msecs)03.0f [%(levelname)] %(message)s'

.. _configuration-options-log-level:

``log-level``
-------------

The level at which to log messages. Possible options are ``CRITIAL``, ``ERROR``,
``WARNING``, ``INFO``, ``DEBUG``.

Default: ``WARNING``.

CLI usage example:

.. code-block:: bash

  $ napalm-logs -l debug
  $ napalm-logs --log-level info

Configuration file example:

.. code-block:: yaml

  log_level: info

.. _configuration-options-port:

``port``
--------

This can be assigned using ``-p``

The port to use to listen for all incoming syslog messages.

Default: ``514``.

CLI usage example:

.. code-block:: bash

  $ napalm-logs -p 1024
  $ napalm-logs --port 1024

Configuration file example:

.. code-block:: yaml

  port: 1024

.. _configuration-options-publish-address:

``publish-address``
-------------------

The IP address to use to output the processed message.

Default: ``0.0.0.0``.

CLI usage example:

.. code-block:: bash

  $ napalm-logs --publish-address 172.17.17.3

Configuration file example:

.. code-block:: yaml

  publish_address: 172.17.17.3

.. _configuration-options-publish-port:

``publish-port``
----------------

The port to use to output the processes message.

Default: ``49017``.

CLI usage example:

.. code-block:: bash

  $ napalm-logs --publish-port  2048

Configuration file example:

.. code-block:: yaml

  publish_port: 2048

.. _configuration-options-transport:

``transport``
-------------

The module to use to output the processed message information. For more details,
see :ref:`publisher`.

Default: ``zmq`` (ZeroMQ).

CLI usage example:

.. code-block:: bash

  $ napalm-logs -t kafka
  $ napalm-logs --transport kafka
  $ napalm-logs --publisher kafka

Configuration file example:

.. code-block:: yaml

  transport: kafka

Or:

.. code-block:: yaml

  publisher: kafka

Config File Only Options
++++++++++++++++++++++++

The options to be used inside of the pluggable modules are not provided via the
command line, they need to be provided in the config file.

.. _configuration-options-device-whitelist:

``device_whitelist``
--------------------

List of platforms to be supported. By default this is an empty list, thus
everything will be accepted. This is useful to control the number of
sub-processes started.

Example:

.. code-block:: yaml

  device_whitelist:
    - junos
    - iosxr

.. _configuration-options-device-blacklist:

``device_blacklist``
--------------------

List of platforms to be ignored. By default this list is empty, thus nothing
will be ignored. This is also useful to control the number of sub-processes
started.

Example:

.. code-block:: yaml

  device_blacklist:
    - eos
