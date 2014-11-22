### Steps to get boundary service up and running

    initdb /usr/local/var/postgres/ -E utf-8
    createdb test_gis
    psql test_gis -c "CREATE EXTENSION postgis;"
    psql test_gis
    select postgis_lib_version();








#### Creating the template spatial database

	createdb -E UTF8 template_postgis
	createlang -d template_postgis plpgsql
	psql -d postgres -c "UPDATE pg_database SET datistemplate='true' WHERE datname='template_postgis';"
	psql -d template_postgis -f ~/Desktop/postgis.sql
	psql -d template_postgis -f ~/Desktop/postgis_comments.sql
	psql -d template_postgis -f ~/Desktop/spatial_ref_sys.sql

#### Enabling users to alter spatial tables.
	psql -d template_postgis -c "GRANT ALL ON geometry_columns TO PUBLIC;"
	psql -d template_postgis -c "GRANT ALL ON geography_columns TO PUBLIC;"
	psql -d template_postgis -c "GRANT ALL ON spatial_ref_sys TO PUBLIC;"

#### Set up postgres geo-spacial database:
	sudo -u KellerUser createuser --createdb testgis_user
	sudo -u KellerUser psql -c "ALTER USER testgis_user with password '1234'";
	sudo -u KellerUser createdb -T template_postgis -O testgis_user testgis_db

#### [Dealing with this error](http://answers.bitnami.org/questions/5283/geodjango-problems-postgis):

	Failed to install index for boundaryservice.Boundary model: operator class "gist_geometry_ops" does not exist for access method "gist"
	No fixtures found.

[patch for error](https://code.djangoproject.com/attachment/ticket/16455/django-trunk-postgis2-version2.0.patch#L46)

[gist of patch](https://raw.github.com/django/django/92b5341b19e9b35083ee671afc2afb2f252c662d/django/contrib/gis/db/backends/postgis/creation.py)

[ticket](https://code.djangoproject.com/ticket/16455)

#### [django-extensions](http://packages.python.org/django-extensions/command_extensions.html)

	pip install django-extensions

**To Reset the database**

	python manage.py reset_db --router=default

#### Postgres 9.2 and PostGIS 2 and Django 1.4 aren't happy with one another
brew install https://raw.github.com/gist/3996154/a8a38d0bdeb363bfe387fc535f8331dd31edc8b9/postgresql916.rb
brew tap homebrew/versions
brew install postgis15

#### [install_postgis_osx.sh](https://gist.github.com/2429181)

#### Fixed this error
    django.db.utils.DatabaseError: invalid byte sequence for encoding "UTF8": 0x00

[This is due an incompatibility](http://wildfish.com/blog/2011/11/9/installing-postgis-ubuntu/) between a change in Postgres 9.1's new default config and Django 1.3. It requires the postgres setting for standard_conforming_string to be off, but it's switched on by default now. You can either set your standard_conforming_string = off in postgres.conf, or you can patch Django. [See here](https://code.djangoproject.com/ticket/16778).

[PostGIS adapter patch](https://code.djangoproject.com/attachment/ticket/16778/postgis-adapter.patch) to fix error