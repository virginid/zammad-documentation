Getting and Updating Zammad-Settings
************************************

.. Note:: Please note that this is not a full setting list, if you're missing settings, feel free to ask over at our `Community <https://community.zammad.org>`_.


Send all outgoing E-Mails to a BCC-Mailbox
------------------------------------------

This option allows you to send all outgoing E-Mails (not notifications) to a specific mailbox.
Please note that this shouldn't be a mailbox you're importing already! This will apply to all groups and is a global setting.
::
 
 Setting.set('system_bcc', 'alias@domain.tld')

You can easilly check the current BCC-Setting by running the following: 
::
 
 Setting.get('system_bcc')


Get ticket_hook setting
-----------------------

This will give you the Ticket hook that you'll find inside the `[]` in front of the ticket number.
By default this will be `Ticket#` - you shouldn't change this setting in a productive system.
::

 Setting.get('ticket_hook')


Get fqdn setting
----------------

Get the current FQDN-Setting of Zammad and, if needed, adjust it.
::

 Setting.get('fqdn')			# Get FQDN
 Setting.set('fqdn', 'new.domain.tld')	# Set a new FQDN


Find storage_provide setting
----------------------------

The following command returns a list of available settings for `storage_provider` (for attachments).
::

 Setting.find_by(name: 'storage_provider')


Set storage_rpovider Setting
----------------------------

Change the storage_provider if needed.
::

 Setting.set('storage_provider', 'DB')	# Change Attachment-Storage to database
 Setting.get('storage_provider')	# get the current Attachment-Storage


Configuring Elasticsearch
-------------------------

If your elasticsearch installation changes, you can use the following commands to ensure that Zammad still can access elasticsearch.
::

 Setting.set('es_url', 'http://127.0.0.1:9200')			# Change elasticsearch URL to poll
 Setting.set('es_user', 'elasticsearch')			# Change elasticsearch user (e.g. for authentication)
 Setting.set('es_password', 'zammad')				# Change the elasticsearch password for authentication
 Setting.set('es_index', Socket.gethostname + '_zammad')	# Change the index name
 Setting.set('es_attachment_ignore', [ '.png', '.jpg', '.jpeg', '.mpeg', '.mpg', '.mov', '.bin', '.exe', '.box', '.mbox' ] )	# A list of ignored file extensions (they will not be indexed)
 Setting.set('es_attachment_max_size_in_mb', 50)		# Limit the Attachment-Size to push to your elasticsearch index


Use the OTRS importer from the shell
------------------------------------

If needed, you can configure and run the OTRS-Import from console.
::

 Setting.set('import_otrs_endpoint', 'http://xxx/otrs/public.pl?Action=ZammadMigrator')
 Setting.set('import_otrs_endpoint_key', 'xxx')
 Setting.set('import_mode', true)
 Import::OTRS.start


Enable proxy
------------

Zammad needs to use a proxy for network communication? Set it here.
::

 Setting.set('proxy', 'proxy.example.com:3128')
 Setting.set('proxy_username', 'some user')
 Setting.set('proxy_password', 'some pass') 


Activate counter on grouped overviews
-------------------------------------

This is a hidden setting which you can only set via Command-Line.
This will globally enable a ticket number value in each heading for grouped elements.
::
  
  Setting.set('ui_table_group_by_show_count', true)	# enable counter on grouped overviews
  Setting.set('ui_table_group_by_show_count', false)	# disable counter on grouped overviews
  Setting.get('ui_table_group_by_show_count')		# get current setting (if NIL, it's false)

.. image:: /images/console/ui_table_group_by_show_count-example.png
 
