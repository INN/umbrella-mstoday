## Setup instructions

This repository is designed to be set up in accordance with the VVV install instructions in INN/docs, that were introduced with https://github.com/INN/docs/pull/148


```
vv create
```

Prompt | Text to enter 
------------ | -------------
Name of new site directory: | mstoday
Blueprint to use (leave blank for none or use largo): | largo
Domain to use (leave blank for largo-umbrella.dev): | mstoday.dev
WordPress version to install (leave blank for latest version or trunk for trunk/nightly version): | *hit [Enter]*
Install as multisite? (y/N): | n
Install as subdomain or subdirectory? : | subdomain
Git repo to clone as wp-content (leave blank to skip): | *hit [Enter]*
Local SQL file to import for database (leave blank to skip): | *This filename must be an absolute path, so the easiest thing to do on a Mac is to drag your mysql file into your terminal window here: the absolute filepath with fill itself in. Absolute filepaths begin from `/` and go all the way to the file.*
Remove default themes and plugins? (y/N): | y
Add sample content to site (y/N): | N
Enable WP_DEBUG and WP_DEBUG_LOG (y/N): | N

After reviewing the options and creating the new install, partake in the following steps:

1. `cd` to the directory `mstoday/` in your VVV setup
2. `git clone git@github.com:INN/umbrella-mstoday.git`
3. Copy the contents of the new directory `umbrella-mstoday/` into `htdocs/`, including all hidden files whose names start with `.` periods.
	- the easy way to do this is: `rsync -rv umbrella-mstoday/ htdocs`
4. `cd htdocs` to move to the folder where the umbrella now lives
5. `git submodule update --init` to pull down all of the submodules you need (including, crucially, the tools repo)
6. `workon fabric`
7. `fab production wp.fetch_sql_dump` (or download via FTP if this doesn't work)
8. `fab vagrant.reload_db:mysql.sql`
9. Search and replace 'mstoday.wpengine.com' --> 'mstoday.dev' in the db (options for doing this are covered in the [largo umbrella setup instructions](https://github.com/INN/docs/blob/master/projects/largo/umbrella-setup.md)
10. Optionally, you may want to pull down recent uploads so you have images, etc. to work with locally.
11. Visit mstoday.dev in your browser and you should see the site!
