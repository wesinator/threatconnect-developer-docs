Create Signatures
^^^^^^^^^^^^^^^^^

The example below demonstrates how to create a Signature Resource in the
ThreatConnect platform.

.. code-block:: python
    :linenos:

    ...

    tc = ThreatConnect(api_access_id, api_secret_key, api_default_org, api_base_url)

    signatures = tc.signatures()
        
    owner = 'Example Community'
    signature = signatures.add('New Signature', owner)

    file_text = '"rule example_sig : example\n{\n'
    file_text += 'meta:\n        description = "This '
    file_text += 'is just an example"\n\n '
    file_text += 'strings:\n        $a = {6A 40 68 00 '
    file_text += '30 00 00 6A 14 8D 91}\n        $b = '
    file_text += '{8D 4D B0 2B C1 83 C0 27 99 6A 4E '
    file_text += '59 F7 F9}\n    condition:\n '
    file_text += '$a or $b or $c\n}"'

    signature.set_file_name('bad_file.txt')
    signature.set_file_type('YARA')
    signature.set_file_text(file_text)
        
    signature.add_attribute('Description', 'Description Example')
    signature.add_tag('EXAMPLE')
    signature.set_security_label('TLP Green')
    try:
        signature.commit()
    except RuntimeError as e:
        print('Error: {0}'.format(e))
        sys.exit(1)

Supported Properties

+-----------------+-------------------+------------+
| Property Name   | Method            | Required   |
+=================+===================+============+
| file\_name      | set\_file\_name   | True       |
+-----------------+-------------------+------------+
| file\_text      | set\_file\_text   | False      |
+-----------------+-------------------+------------+
| file\_type      | set\_file\_type   | True       |
+-----------------+-------------------+------------+

.. note:: In the prior example, no API calls are made until the ``commit()`` method is invoked.

Code Highlights

+----------------------------------------------+------------------------------------------------------------------+
| Snippet                                      | Description                                                      |
+==============================================+==================================================================+
| ``tc = ThreatConnect(api_access_id, api...`` | Instantiate the ThreatConnect object.                            |
+----------------------------------------------+------------------------------------------------------------------+
| ``signatures = tc.signatures()``             | Instantiate a Signatures container object.                       |
+----------------------------------------------+------------------------------------------------------------------+
| ``signature = signatures.add('New Signa...`` | Add a Resource object setting the name and Owner.                |
+----------------------------------------------+------------------------------------------------------------------+
| ``signature.set_file_name('bad_file.txt')``  | **(REQUIRED)** Set file name for Signature.                      |
+----------------------------------------------+------------------------------------------------------------------+
| ``signature.set_file_type('YARA')``          | **(REQUIRED)** Set file type for Signature.                      |
+----------------------------------------------+------------------------------------------------------------------+
| ``signature.set_file_text(file_text)``       | **(OPTIONAL)** Set file contents for Signature.                  |
+----------------------------------------------+------------------------------------------------------------------+
| ``signature.add_attribute('Description'...`` | Add an Attribute of type **Description** to the Resource.        |
+----------------------------------------------+------------------------------------------------------------------+
| ``signature.add_tag('EXAMPLE')``             | Add a Tag to the Signature.                                      |
+----------------------------------------------+------------------------------------------------------------------+
| ``signature.set_security_label('TLP Gre...`` | Add a Security Label to the Signature.                           |
+----------------------------------------------+------------------------------------------------------------------+
| ``signature.commit()``                       | Trigger API calls to write all added, deleted, or modified data. |
+----------------------------------------------+------------------------------------------------------------------+