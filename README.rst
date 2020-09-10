=============
CKAN Rating extension
=============

This is a simple rating extension for CKAN datasets (packages) and showcases. The extension adds a list of clickable stars to the side navigation
in the dataset and showcacse templates similar to ckanext-qa. In showcase the stars are also displayed in the showcase listing, but are not clickable.

The stars can also be added to any desired view by adding the following code to the desired template::

    {% snippet "rating/snippets/stars.html", package=<YOUR_PACKAGE> %}

The amount of ratings submitted can also be displayed with::

    {{h.package_rating(None, {'package_id' : <YOUR_PACKAGE>.id} ).ratings_count}}

Rating is identified with client IP if the user is not authenticated. User ID is saved with the rating when authenticated.


------------
Requirements
------------

This extension works with CKAN version 2.8.5


------------
Installation
------------

To install ckanext-rating:

1. Activate your CKAN virtual environment, for example::

     . /usr/lib/ckan/default/bin/activate

2. Install the ckanext-rating Python package into your virtual environment::
	
	cd /usr/lib/ckan/default/src
    git clone https://github.com/localidata/ckanext-rating
	cd ckanext-rating
	pip install -r dev-requirements.txt	 
	python setup.py develop
	//python setup.py develop --uninstall

	

3. Add ``rating`` to the ``ckan.plugins`` setting in your CKAN
   config file (by default the config file is located at
   ``/etc/ckan/default/production.ini``).

4. Restart CKAN. For example if you've deployed CKAN with Apache on Ubuntu::

     sudo service apache2 restart

5. Initialize database tables used by Rating::

    paster --plugin=ckanext-rating rating init --config=/etc/ckan/default/production.ini

6. If you want to use this extension for ckanext-showcase, install it into your environment by following the instructions at https://github.com/ckan/ckanext-showcase

Uninstall
------------

To uninstall ckanext-rating:

1. Activate your CKAN virtual environment, for example::

     . /usr/lib/ckan/default/bin/activate
	 
2. Go to the extension path

	 cd /usr/lib/ckan/default/src/ckanext-rating

3. Uninstall

	 python setup.py develop --uninstall
	 
4. Erase  extension folder

	 rm -r /usr/lib/ckan/default/src/ckanext-rating
	 
5. Erase 'rating' from  the plugin list in production.ini

	 
6. Restart CKAN. For example if you've deployed CKAN with Apache on Ubuntu::

     sudo service apache2 restart 

---------------
Config Settings
---------------

Rating is enabled or disabled for unauthenticated users::

  rating.enabled_for_unauthenticated_users = true or false

Optional::

    # List of dataset types for which the rating will be shown (defaults to ['dataset'])
    ckanext.rating.enabled_dataset_types


