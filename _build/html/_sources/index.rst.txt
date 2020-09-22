Rest Routes Pro
===========================================

Rest Routes Pro is a WordPress plugin that lets you extend the WordPress REST API. You can build complexes
custom endpoints for native WordPress objects (posts, taxonomies, users, custom fields) as well as for
any custom database table.

The beauty of the plugin is that you don't need to touch a single line of PHP code for that. It comes out
with a well-designed interface for building your custom endpoints.

Who is that For
================

**Front-end Developers**

If you are a WordPress front-end developer or a mobile developer that uses WordPress as a back-end service you would take a lot from Rest Routes. You can build your front-end applications using any framework of your choice (React, Vue, etc.) and then use Rest Routes to design the custom endpoints that they will consume without the need of touching PHP code for it.

**Integration with third-party APIs**

This plugin is recommended for you that is developing WordPress applications that need to communicate with external servers. You can easily build custom routes that will both expose data to the third-party server and populate data into your WordPress application database.

**WordPress Headless Applications**

If you are simply using the WordPress as a back-end application, which means that you are not using anything related to the front-end of the WordPress, such as Themes, then this plugin is fully recommended for you. You can easily build custom routes that will let you expose your back-end data and also populate existing database tables.

Custom Endpoints
==================

You can easily find all the custom routes that you previously created through Rest Routes Pro as well as
add a new one through the WordPress admin menu **Rest Routes Pro > Routes**.

Basic Settings
----------------

This is the first section that you will find once editing or creating a new route. There you will find two
text fields:

**Namespace**

Namespaces are the first part of the URL for the endpoint. They should be used as a vendor/package prefix to prevent clashes between custom routes. Namespaces allows for two plugins to add a route of the same name, with different functionality.

Namespaces in general should follow the pattern of vendor/v1, where vendor is typically your plugin or theme slug, and v1 represents the first version of the API. If you ever need to break compatibility with new endpoints, you can then bump this to v2.

**Route name**

This is the second part of the custom endpoint and the name of your route that comes out just after the namespace. So given the route below:

`wp-json/acme/v1/some-nice-route`

The namespace is `acme/v1` and the route name `some-nice-route`.

Visibility
-----------

First of all, you must understand that for each single route you can have many endpoints. So, for instance,
for the route above `wp-json/acme/v1/some-nice-route` you can have one endpoint for displaying some posts
using the HTTP GET method and another endpoint for creating posts using the HTTP POST method.

Knowing that, you can whether switch the visibility of your entire route (both endpoints) or only switch
the visibility of some particular endpoint.

For doing that, you must use the green switcher for enabling or disabling.

Once you do that, the selected endpoints or the entire route won't be registered on the list of available
WP REST endpoints anymore, until you enable them again.

Methods
----------

This is the first left box that you will find once editing or creating a new route. There is where you can
define which HTTP method you are going to use. You can have up to 4 endpoints on each route and each
endpoints should be using a different method. Which means that you can't have the same HTTP method for
two or more custom endpoints.

In order to follow the recommended practices when working with REST APIs, remember to always use the right
method for your endpoints:

- GET: for displaying resources
- POST: for creating resources
- PUT: for editing resources
- DELETE for deleting resources

**This is a required field, you can't have one endpoint without a method**

.. _`source field`:

The Source Field
-----------------

When creating your custom routes, you will notice that several fields in many places
contains a field called **Source**. This where you can give a **Fixed Value** or a **Dynamic** (Custom Parameters, see `custom parameters`_).

These fields can be found on many places, such as:

- Default filters (e.g.: post id, post type)
- Custom fields filters
- Taxonomies filters
- Custom table filters
- Limit and offset
- and much more

These fields are the ones responsible by customizing your endpoint and that can be by adding some filter or maybe limiting
the number of posts displayed through the endpoint.

If you select the **Fixed Value** option, you will need to provide some value for your field and this value will
be always used whenever this endpoint will be called.

If you select the **Custom Parameter**, then it will prepare the endpoint for receiving the information
from the end user. See the `custom parameters`_ section for understanding better how Custom Parameters work.

.. _`multiple values`:

Multiple-values Field
---------------------

Those fields accept one or more values. If you defined the `source field`_ of it as **Fixed Value** you can separate the values using comma. When you define it as `custom parameter`_ you can
pass array arguments in the request, something like: **your-url.dev/arg[]=1&arg[]=2&arg[]=3**

.. _`custom parameter`:
.. _`custom parameters`:

Custom Parameters
------------------

This is a very important part of the plugin. This is where you can define custom parameters that can be
used by end users to interact with your custom endpoints.

In order to use that, first of all you must add it using the **Custom Parameters** section. There are a couple
of settings you can define for each parameter:

- Name: the way to identify your parameter and also the name that end users will use
- Type: you can force a type for your parameter
- Required: marking this option will deny requests that are not passing this parameter
- Default: you can put any default value for your parameter here to be used in case of missing it

After defining the custom parameter it is time to use that somewhere and that you already learned in the `source field`_ section.

Endpoint Privacy
-----------------

Your custom routes can be whether protected or public. If don't want to protect your custom route, then you can
simply ignore this section.

If you want to protect that, then you can choose some capability in the **Endpoint Privacy** section.

For creating custom routes that only administrators can access, you could choose the `manage_options` capability.
This would make the request fail if the logged user has no capability of `manage_options` (non-administrators).

**One very important note here is that you must use a third-party plugin for handling the authentication of
your REST requests (JWT, OAuth).**

Endpoint Type
---------------

This is a key part of the plugin, where you will define the purpose of your endpoint. There are distinct options available
for every Endpoint Type. So, as soon as you switch the type, the right options will be displayed to you.

Posts
+++++++++

You will see on this section endpoint types responsible for creating endpoints for posts as well as associated custom fields and taxonomies.

Display Posts
***************

This should be used for outputting posts as well as associated custom fields and taxonomies.

.. note:: We recommend to use the GET method for this endpoint type in order to follow the best REST practices.

Once you select this Endpoint Type you will find several options that will let you completely customize your endpoint. Those options will let you
refine the results that this endpoint will output:

**Default Fields Filter**

Here you can add many filters for different default post fields.

- **Status**: the status of the post (published, draft, private, etc)
- **Type**: the post type of the post (post, page, product, etc)
- **Title**: the exact title of the post
- **ID**: the id of the post. It accepts `multiple values`_
- **ID not**: the id of the post you don't want to return. It accepts `multiple values`_
- **Page name**: the name of the page. It accepts `multiple values`_
- **Author ID**: the id of the post's author. It accepts `multiple values`_
- **Author ID not in**: the id of the post's author you don't want to return. It accepts `multiple values`_
- **Author name**: the post's author name.
- **Parent ID**: the post's parent ID. It accepts `multiple values`_
- **Parent ID not in**: the post's parent id you don't want to return. It accepts `multiple values`_
- **Post search**: the keywords passed here will be used to look for post by the post title or post content (default WordPress search mechanism)

Once you choose a filter you will see a field called `source field`_, you should choose the right option accordingly to your needs.

**Query Groups**

See the `query groups`_ section for more information about this one.

**Custom Fields Filter**

See the `custom fields`_ section for more information about this one.

**Taxonomies Filter**

This one is used for adding filters for multiple taxonomies, in case you want to display posts based in one or more terms. Same as the custom fields section
here you can add as many filters as you want for the taxonomies and each filter contains a set of fields:

- **Source** (see `source field`_)
- **Taxonomy**: the taxonomy that you want to add the filter for
- **Field type**: the term field that you want to add the filter for, possible values are: Term ID, Name and Slug
- **Query Group**: this field appears only when there is a query group already defined. For more details about this one please check the `query groups`_ section

**Ordering**

See the `ordering`_ section for more information about this one.

**Limit and Offset**

See the `limit and offset`_ section for more information about this one.

**Output**

On this section you are able to choose which fields you will want to output through the endpoint. By default, all default fields are outputted. Below you will find
the complete list of fields that you can expose:

- Title
- ID
- Author
- Date
- Date GMT
- Content
- Excerpt
- Status
- Comment status
- Ping status
- Password
- Name
- To ping
- Pinged
- Modified date
- Modified date GMT
- Content filtered
- Parent
- GUID
- Permalink
- Menu order
- Post type
- Post mime type
- Comment count
- Post format
- Custom field: **this option requires you to fill the field "Custom field name" in order to inform the endpoint which custom field you will want to display**
- Taxonomy: **this option requires you to fill some fields in order to inform the endpoint which taxonomy term you will want to display**
- Featured image
- Attached images
- Attached audios
- Attached videos

Edit Posts
***********

This endpoint type can be used to edit some post as well as associated custom fields and taxonomy terms.

.. note:: We recommend you to choose the **Editable** method which can be POST, PUT or PATCH in order to follow the best REST practices.

**Default Fields**

The very first thing you should do is to define how the endpoint will find the ID of the post to be edited. For this, you have a default field that contains only the `source field`_.

See below the complete list of fields that can be edited through this endpoint type:

- Title
- Content
- Excerpt
- Date
- Password
- Parent
- Menu order
- Status
- Type
- Author

Once you choose a filter you will see a field called `source field`_, you should choose the right option accordingly to your needs and this will inform
the endpoint how it will populate the post fields.

**Custom Fields**

This section lets you update associated custom fields. If the custom field is not already associated to the post then a new custom field is added and connected.

For each custom field you will have to fill two fields, the `source field`_ and "Custom field name". This is required in order to inform the endpoint
how to populate the custom field when editing the post.

Notice that you can add as many custom fields as you need.

**Taxonomies**

This section lets you update the associated taxonomy terms exactly like in the Custom Fields section.

There is an extra option that lets you choose whether you want to append the term to already associated terms or simply disconnect other terms and let only
the new one associated to the post.

For each taxonomy you will have to fill a few fields, the `source field`_, the "Taxonomy" which is the taxonomy type and "Field type" which is
the field used to match the taxonomy term and associate it. This is required in order to inform the endpoint
how to populate the taxonomy term when editing the post.

Create Posts
*************

This endpoint type should be used to create new posts as well as associate custom fields and taxonomy terms.

.. note:: We recommend to use the **Creatable** method which is POST in order to follow the best REST practices.

**Default Fields**

See below the list of fields that can be filled when creating a new post through the endpoint:

- Title
- Content
- Excerpt
- Date
- Password
- Parent
- Menu order
- Status
- Type
- Author

For each default field you will have to select the `source field`_ accordingly to the way you want to populate the field of the new post.

**Custom Fields**

When adding a new post through your custom endpoint you will also be able to associate custom fields to it.

For each custom field you will have to fill two fields, the `source field`_ and "Custom field name". This is required in order to inform the endpoint
how to populate the custom field when creating the new post.

**Taxonomies**

When creating a new post you will also be able to associate taxonomy terms or create a new ones and associate to the newly created post.

For each taxonomy you will have to fill a few fields, the `source field`_, the "Taxonomy" which is the taxonomy type and "Field type" which is
the field used to match the taxonomy term and associate it. This is required in order to inform the endpoint
how to populate the taxonomy term when creating the new post.

Taxonomies
+++++++++++

On this section you will see the endpoint types responsible for creating endpoints for taxonomy terms.

Display Taxonomies
*******************

This endpoint type should be used whenever you need to display taxonomy terms as well as associated term meta fields.

.. note:: We recommend to use the GET method for this endpoint type in order to follow the best REST practices.

**Query Groups**

See the `query groups`_ section for more information about this one.

**Custom Fields Filter**

See the `custom fields`_ section for more information about this one.

**Ordering**

See the `ordering`_ section for more information about this one.

**Limit and Offset**

See the `limit and offset`_ section for more information about this one.

**Endpoint Output**

On this section you can define which term fields you will want to output through your endpoint. By default, all the term fields will be outputted.

See below the list of available fields:

- Term ID
- Name
- Slug
- Term group
- Taxonomy ID
- Description
- Count
- Custom field: **this is a special field, if you choose this one you will need to also fill a new field called "Custom field name"**

Users
+++++++++++

Now it's time to learn about the endpoint types responsible by handling actions on users as well as connected user meta fields.

Display Users
***************

This endpoint type should be used whenever you need to output information about users.

.. note:: We recommend to use the GET method for this endpoint type in order to follow the best REST practices.

**Default Fields Filter**

Here is where you can add filters for default user fields, this will let you refine the results of your endpoint.

- User ID in: It accepts `multiple values`_
- User login
- User nice name
- Roles: It accepts `multiple values`_
- User email
- User URL
- User registered
- User status
- User display name
- Roles in: It accepts `multiple values`_
- Blog ID
- Has published posts
- User ID not in: It accepts `multiple values`_

Once you choose a filter you will see a field called `source field`_, you should choose the right option accordingly to your needs.

**Query Groups**

See the `query groups`_ section for more information about this one.

**Custom Fields Filter**

See the `custom fields`_ section for more information about this one.

**Ordering**

See the `ordering`_ section for more information about this one.

**Limit and Offset**

See the `limit and offset`_ section for more information about this one.

**Endpoint Output**

Here is where you define which user fields should be outputted, by default all the user fields will outputted. See below the list of fields available:

- User ID
- User login
- User nice name
- User role
- User email
- User URL
- User registered
- User status
- User display name
- Custom field: **this is a special field, if you choose this one you will need to also fill a new field called "Custom field name"**

Create Users
**************

This endpoint type is the one that should be used for creating new users.

.. note:: We recommend you to choose the **Creatable** method which POST in order to follow the best REST practices.

**Default Fields**

On this section is where you say how the default user fields should be populated when adding new users through the endpoint. The available fields are:

- User login
- User nice name
- User role
- User email
- User URL
- User status
- User display name
- User password

Once you choose an user field you will see a field called `source field`_, you should choose the right option accordingly to your needs and this will tell the endpoint
how to retrieve the data for the user fields when creating new users.

**Custom Fields**

When adding a new user through your custom endpoint you will also be able to associate custom fields to it.

For each custom field you will have to fill two fields, the source field and "Custom field name". This is required in order to inform the endpoint how to populate the custom field when creating the new user.

Edit Users
***********

This endpoint type can be used to edit some user as well as associated custom fields.

.. note:: We recommend you to choose the **Editable** method which can be POST, PUT or PATCH in order to follow the best REST practices.

**Default Fields**

The very first thing you should do is to define how the endpoint will find the ID of the user to be edited. For this, you have a default field that contains only the `source field`_.

See below the complete list of fields that can be edited through this endpoint type:

- User nice name
- User role
- User email
- User URL
- User status
- User display name

Once you choose a filter you will see a field called `source field`_, you should choose the right option accordingly to your needs and this will inform
the endpoint how it will populate the user fields.

**Custom Fields**

This section lets you update associated custom fields. If the custom field is not already associated to the user then a new custom field is added and connected.

For each custom field you will have to fill two fields, the `source field`_ and "Custom field name". This is required in order to inform the endpoint
how to populate the custom field when editing the user.

Notice that you can add as many custom fields as you need.

Custom Tables
+++++++++++++++

WordPress database structure is very powerful, however, sometimes we still need to create custom tables maybe because of performance or for filling a very particular
need.

Rest Routes is fully compatible with custom tables, which means that you can create custom endpoints for doing anything with custom tables.

Display Items
***************

This is the endpoint type that can be used whenever you need to display items from custom tables.

.. note:: We recommend you to choose the **Readable** method which is GET in order to follow the best REST practices.

**Table Selection**

This is a required section, where you should choose which table you will want to output data.

**Filter Columns**

On this section you can add filters for the table columns as well as choose the relation type (AND | OR). You can add as many filters as you need and that
will refine the results that your endpoint will output.

**Ordering**

See the `ordering`_ section for more information about this one.

**Limit and Offset**

See the `limit and offset`_ section for more information about this one.

**Endpoint Output**

Here is where you can define which columns of the table should be displayed in the output. By default all the columns will be displayed.

Create Items
*******************

This endpoint type should be used whenever you need to create items on custom tables.

.. note:: We recommend you to choose the **Creatable** method which is POST in order to follow the best REST practices.

**Table Selection**

This is a required section, where you should choose which table you will want to create data.

**Columns to Populate**

Here you should define how you will populate the columns of the custom table.

Once you choose a column you will see a field called `source field`_, you should choose the right option accordingly to your needs and this will inform
the endpoint how it will populate the custom table field.

Edit Items
***********

**Table Selection**

This is a required section, where you should choose which table you will want to edit data.

.. note:: We recommend you to choose the **Editable** method which can be POST, PUT or PATCH in order to follow the best REST practices.

.. warning:: This is a dangerous endpoint type! You must be sure of what you are doing. This endpoint will let you delete both single and a range of entries from any kind of database table, even default WordPress ones. So, pay attention specially to the Filters section and always make database backup.

**Columns to Edit**

On this section you will tell the endpoint which columns should be updated and how.

Once you choose a column you will see a field called `source field`_, you should choose the right option accordingly to your needs and this will inform
the endpoint how it will populate the custom table fields.

**Filters**

On this section is where you should adjust the range of affected custom table entries. You can add as many filters as you need as well as adjust the relation type
(AND | OR).

Once you choose a column you will see a field called `source field`_, you should choose the right option accordingly to your needs and this will inform
the endpoint how it will populate the custom table field.

Delete Items
*************

This endpoint type should be used for deleting entries from custom tables.

.. note:: We recommend you to choose the **Deletable** method which DELETE in order to follow the best REST practices.

.. warning:: This is a dangerous endpoint type! You must be sure of what you are doing. This endpoint will let you delete both single and a range of entries from any kind of database table, even default WordPress ones. So, pay attention specially to the Filters section and always make database backup.

**Table Selection**

This is a required section, where you should choose which table you will want to edit data.

**Filters**

This section is the one which will limit the range of affected entries.

Once you choose a column you will see a field called `source field`_, you should choose the right option accordingly to your needs and this will inform
the endpoint how it will retrieve the custom table column data.

.. _`query groups`:

Query Groups
--------------

Query groups are options that will appear when you are dealing with filters for Custom Fields and Taxonomies. This is a way of dealing with complexes queries, so you can
break the filter in two or more groups.

When working with **WP_Query** the `meta_query` clauses can be nested in order to construct complex queries.
For example, for showing products where **color=orange** OR **color=red&size=small** translates to the following in code:

::

    $args = array(
      'post_type'  => 'product',
      'meta_query' => array(
          'relation' => 'OR',
          array(
              'key'     => 'color',
              'value'   => 'orange',
              'compare' => '=',
          ),
          array(
              'relation' => 'AND',
              array(
                      'key' => 'color',
                      'value' => 'red',
                      'compare' => '=',
              ),
              array(
                      'key' => 'size',
                      'value' => 'small',
                      'compare' => '=',
              ),
            ),
      ),
    );

    $query = new WP_Query( $args );

To achieve that with Rest Routes, you should:

- In the **Query Groups** section add a new group choosing the relation field as **AND**
- Set the **Main relation type** field under Custom Fields section to **OR**
- Add a custom field filter for **color**
- Add a new custom field filter for **color** and choose the group you already created
- Add a new custom field filter for **size** and also choose the same group like above

.. _`custom fields`:

Custom Fields Filter
---------------------

Here is where you can add filters for your posts based on values of associated custom fields. You can add as many filters of this kind as you want
and each one has a set of fields:

- **Source** (see `source field`_)
- **Custom field name**: the exact custom field key stored in the database
- **Compare**: the comparison type for the custom field
- **Type**: the type that the query should treat this field
- **Query Group**: this field appears only when there is a query group already defined. For more details about this one please check the `query groups`_ section

Ordering
----------

This one should be used to define an order for the items that you are outputting which can be posts, terms, users, custom table items, etc. You have two group of fields
that you should fill:

- **Order by**

  - Source: (see `source field`_)
  - Order by: this is the field that you want to order your results by. It can be default fields or even a custom field
- **Order**:

  - Source: (see `source field`_)
  - Order: here you can define the direction of the ordering which can be **ASC** or **DESC**

Limit and Offset
-----------------

On this section is where you define how many items you want to display through the endpoint and also how many items you want to skip. Both group of fields contains only one field
which is the `source field`_.

This is very handy for paginating items! You can set the limit by 10 and skip items per some `custom parameter`_. So, depending on the custom parameter
value that the end user will pass to the endpoint, it will skip **X** posts thus producing a pagination effect.

Third-party Compatibility
===========================

Currently, Rest Routes is compatible with the following plugins:

- ACF
- Toolset Types

Hooks
========

Actions
--------

Posts
++++++

**rest_routes_before_create_posts_callback**

Called right before the creation of posts. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_after_create_posts_callback**

Called right after the creation of posts. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_before_edit_posts_callback**

Called right before editing a post. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_after_edit_posts**

Called right after editing a post. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object
- id: the id of the edited post

Taxonomies
+++++++++++

Users
++++++

**rest_routes_before_create_users( $data, $endpoint )**

Called right before the creation of users. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_after_create_users( $data, $endpoint )**

Called right after the creation of users. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_before_edit_user( $data, $endpoint )**

Called right before editing the user. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_after_edit_user( $data, $endpoint, $id )**

Called right after editing the user. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object
- id: the id of the edited user

Custom Tables
++++++++++++++

**rest_routes_before_create_custom_table( $data, $endpoint )**

Called right before the creation of items on custom table. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_after_create_custom_table( $data, $endpoint, $id )**

Called right after the creation of items on custom table. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object
- id: the id of the newly created item

**rest_routes_before_delete_custom_table( $data, $endpoint )**

Called right before deleting custom table items. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_after_delete_custom_table( $data, $endpoint )**

Called right after deleting custom table items. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_before_edit_custom_table_callback( $data, $endpoint )**

Called right before editing custom table items. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_after_edit_custom_table_callback( $data, $endpoint )**

Called right after editing custom table items. Parameters:

- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

Filters
-------

Posts
++++++

**rest_routes_should_process_tax_on_post_creation( true, $endpoint, $data, $id )**

It lets you decide if taxonomies should be processed on post creation. Parameters:

- choice: the filtered boolean value which by default is *true*
- endpoint: the endpoint object
- data: the `\WP_REST_Request` object
- id: the id of the newly created post

**rest_routes_should_process_cf_on_post_creation( true, $endpoint, $data, $id )**

It lets you decide if custom fields should be processed on post creation. Parameters:

- choice: the filtered boolean value which by default is *true*
- endpoint: the endpoint object
- data: the `\WP_REST_Request` object
- id: the id of the newly created post

**rest_routes_create_posts_result( $result, $data, $endpoint, $id )**

It lets you filter the result of the endpoint for creation of posts. Parameters:

- result: the variable that can be filtered which by default is a message containing the id of the newly created post
- data: the `\WP_REST_Request` object
- endpoint: the endpoint object
- id: the id of the newly created item

**rest_routes_display_posts_results( $result, $data, $endpoint )**

It lets you filter the result of the endpoint for displaying posts. Parameters:

- result: the variable that can be filtered which by default is an array of objects
- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_should_process_tax_on_post_edit( true, $endpoint, $data, $id )**

It lets you decide if taxonomies should be processed when editing a post. Parameters:

- choice: the filtered boolean value which by default is *true*
- endpoint: the endpoint object
- data: the `\WP_REST_Request` object
- id: the id of the newly created post

**rest_routes_should_process_cf_on_post_edit( true, $endpoint, $data, $id )**

It lets you decide if custom fields should be processed when editing a post. Parameters:

- choice: the filtered boolean value which by default is *true*
- endpoint: the endpoint object
- data: the `\WP_REST_Request` object
- id: the id of the newly created post

**rest_routes_edit_post_result( $result, $data, $endpoint, $id )**

It lets you filter the result of the endpoint for editing a post. Parameters:

- result: the variable that can be filtered which by default is an array containing the id of the edited post
- data: the `\WP_REST_Request` object
- endpoint: the endpoint object
- id: the id of the edited post

Taxonomies
+++++++++++

**rest_routes_display_taxonomies_results( $result, $data, $endpoint )**

It lets you filter the result of the endpoint for displaying taxonomy terms. Parameters:

- result: the variable that can be filtered which by default is an array of objects
- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

Users
++++++

**rest_routes_should_process_cf_on_user_create( true, $endpoint, $data, $id )**

It lets you decide if custom fields should be processed on user creation. Parameters:

- choice: the filtered boolean value which by default is *true*
- endpoint: the endpoint object
- data: the `\WP_REST_Request` object
- id: the id of the newly created user

**rest_routes_create_users_result( $result, $data, $endpoint, $id )**

It lets you filter the result of the endpoint for creation of users. Parameters:

- result: the variable that can be filtered which by default is an array containing the id of the newly created item
- data: the `\WP_REST_Request` object
- endpoint: the endpoint object
- id: the id of the newly created item

**rest_routes_display_users_results( $result, $data, $endpoint )**

It lets you filter the result of the endpoint for displaying users. Parameters:

- result: the variable that can be filtered which by default is an array of objects
- data: the `\WP_REST_Request` object
- endpoint: the endpoint object

**rest_routes_edit_post_result( $result, $data, $endpoint, $id )**

It lets you filter the result of the endpoint for editing an user. Parameters:

- result: the variable that can be filtered which by default is an array containing the id of the edited user
- data: the `\WP_REST_Request` object
- endpoint: the endpoint object
- id: the id of the edited user

Custom Tables
++++++++++++++

**rest_routes_create_custom_table_result( $result, $data, $endpoint, $id )**

It lets you filter the result of the endpoint for creation of items in custom table. Parameters:

- result: the variable that can be filtered which by default is an array containing the id of the newly created item
- data: the `\WP_REST_Request` object
- endpoint: the endpoint object
- id: the id of the newly created item

**rest_routes_display_custom_table_results( $result, $data, $endpoint )**

It lets you filter the result of the endpoint for displaying items from custom tables. Parameters:

- result: the variable that can be filtered which by default is an array of objects
- data: the `\WP_REST_Request` object
- endpoint: the endpoint object
