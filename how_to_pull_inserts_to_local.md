# How to Recreate a UAT/PAT/PROD Environment Locally

## Part 1: Pulling Inserts

To pull inserts and recreate a project env locally, we first run a `make setup` to set up our project locally, as usual.

In order to recreate the environment locally, we need to login to Teleport and grab data from each of the following tables:
 

		'sys_workflow'
		'sys_translation',
		'sys_transition',
		'sys_condition',
		'sys_state',
		'sys_condition_type',
		'sys_filter',
		'sys_filter_child',
		'sys_filter_group',
		'sys_assignment_action',
		'sys_automated_todo_action',
		'sys_field_value_action',
		'sys_notification_action',
		'sys_schedule_purge_action',
		'sys_rule',
		'sys_workflow',
		'sys_user_role',
		'sys_permission',
		'sys_role_permission',
		'sys_role_filter',
		'sys_list',
		'sys_listitem',
		'sys_grid_column',
		'sys_grid_data_filter',
		'sys_grid_data_filter_child',
		'sys_grid_filter',
		'sys_flag',
		'sys_entity_evaluator',
		'isight_entity',
		'isight_field',
		'isight_dynamic_entity_field',
		'isight_dynamic_entity',
		'sys_layout',

We can do this by completing the next series of steps:
#### Step 1:
In the db container for your project, navigate to `/var/isight/backup`
>`cd /var/isight/backup/`
#### Step 2:
run the command: `ls`

#### Step 3:
if you don’t see an `external-dumps` directory,
run the command: `mkdir external-dumps`

#### Step 4: 
Great, now navigate to the service box and docker exec into the worker.
> `docker exec -it <id of worker container> bash`

#### Step 5: 
You will need to run _**each**_ of the following list of commands to strip files from the db.   

> Make sure you update each of these commands with the **current date**, 
> for example if its **November 8th, 2023**, I would update the filename in each to: **sys_workflow_2023-11-08-231108.sql** 

> Please use a code editor to change them all at once, make your life easier


	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_workflow isight > /usr/local/data/db/external-dumps/sys_workflow_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_translation isight > /usr/local/data/db/external-dumps/sys_translation_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_state isight > /usr/local/data/db/external-dumps/sys_state_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_transition isight > /usr/local/data/db/external-dumps/sys_transition_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_condition isight > /usr/local/data/db/external-dumps/sys_condition_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_condition_type isight > /usr/local/data/db/external-dumps/sys_condition_type_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_filter isight > /usr/local/data/db/external-dumps/sys_filter_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_filter_child isight > /usr/local/data/db/external-dumps/sys_filter_child_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_filter_group isight > /usr/local/data/db/external-dumps/sys_filter_group_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_assignment_action isight > /usr/local/data/db/external-dumps/sys_assignment_action_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_document_action isight > /usr/local/data/db/external-dumps/sys_document_action_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_permission isight > /usr/local/data/db/external-dumps/sys_permission_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_automated_todo_action isight > /usr/local/data/db/external-dumps/sys_automated_todo_action_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_field_value_action isight > /usr/local/data/db/external-dumps/sys_field_value_action_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_notification_action isight > /usr/local/data/db/external-dumps/sys_notification_action_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_schedule_purge_action isight > /usr/local/data/db/external-dumps/sys_schedule_purge_action_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_rule isight > /usr/local/data/db/external-dumps/sys_rule_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_workflow isight > /usr/local/data/db/external-dumps/sys_workflow_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_user_role isight > /usr/local/data/db/external-dumps/sys_user_role_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_role_permission isight > /usr/local/data/db/external-dumps/sys_role_permission_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_role_filter isight > /usr/local/data/db/external-dumps/sys_role_filter_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_list isight > /usr/local/data/db/external-dumps/sys_list_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_listitem isight > /usr/local/data/db/external-dumps/sys_listitem_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_grid_column isight > /usr/local/data/db/external-dumps/sys_grid_column_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_grid_data_filter isight > /usr/local/data/db/external-dumps/sys_grid_data_filter_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_grid_data_filter_child isight > /usr/local/data/db/external-dumps/sys_grid_data_filter_child_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_grid_filter isight > /usr/local/data/db/external-dumps/sys_grid_filter_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_flag isight > /usr/local/data/db/external-dumps/sys_flag_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_entity_evaluator isight > /usr/local/data/db/external-dumps/sys_entity_evaluator_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=isight_entity isight > /usr/local/data/db/external-dumps/isight_entity_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=isight_field isight > /usr/local/data/db/external-dumps/isight_field_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=isight_dynamic_entity_field isight > /usr/local/data/db/external-dumps/isight_dynamic_entity_field_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=isight_dynamic_entity isight > /usr/local/data/db/external-dumps/isight_dynamic_entity_2023-11-08-231108.sql
	PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_layout isight > /usr/local/data/db/external-dumps/sys_layout_2023-11-08-231108.sql

### Step 6:
After running each of these from the worker, go back to the db box, and navigate to the external-dumps directory from earlier.   
> Run this command: `ls -halt`  

You should now see all the files you just created from the worker.

![Screen Shot 2023-11-08 at 3 12 14 PM](https://github.com/CExKForsyth/kyle_notes/assets/95767293/d1415970-83ea-4f4a-817c-e3f6bb4c2556)

### Step 7:
Now we compile them into a zip file. 
> This is where the date is important.   

From this directory, run the following command to create a zip file, but use the same date as the created files:

	find *2023-11-08* -exec tar -rvf archive-nov-08.tar.gz {} --strip-components=1 \;  
> Make sure to also change the date in the archive file name to match the date of the field as well  

### Step 8:
Now download the created zip file.

There, we've pulled the inserts successfully, now we need to use this archive locally.

## Part 2: Recreating the Environment Locally

### Step 1:
Move the downloaded archive file to your desktop, and unzip it.   

### Step 2:
Now open the directory in VSCODE.

### Step 3:
Create a new file at the base of the directory called `script.js`  In this file, add this code:  

	const fs = require('fs');
	fs.readdir('./', (error, files) => {
		console.log('files:', files);
		files.forEach(file => {
    			if(file.includes('.sql')){
        			console.log(``cat /Users/✺✺✺✺✺✺✺✺/Desktop/archive-nov-08/${file} | PGPASSWORD=postgres  psql  -h 127.0.0.1 -p 5432 -U postgres --set ON_ERROR_STOP=on isight``);
    			}
		})
	});

> Make sure to change the path the match your path, with your local username replacing ✺✺✺✺✺✺✺✺✺, and the archive zip file name after Desktop/_________.

### Step 4:
Now create a new empty file in the base of the directory called `cat.txt`  

### Step 5:
Open the VSCode terminal, and from the base of this directory, run: `node script.js`  

### Step 6:
Copy the entire result from your terminal, and past the entire result into `cat.txt`. 
> Save this file.

### Step 7:
Now create another new file in the base of the directory called `delete.txt` 

### Step 8: 
Paste all of these queries into `delete.txt`:  

	DELETE FROM sys_workflow WHERE 1 = 1;
	DELETE FROM sys_translation WHERE 1 = 1;
	DELETE FROM sys_transition WHERE 1 = 1;
	DELETE FROM sys_state WHERE 1 = 1;
	DELETE FROM sys_condition WHERE 1 = 1;
	DELETE FROM sys_condition_type WHERE 1 = 1;
	DELETE FROM sys_filter WHERE 1 = 1;
	DELETE FROM sys_filter_child WHERE 1 = 1;
	DELETE FROM sys_filter_group WHERE 1 = 1;
	DELETE FROM sys_assignment_action WHERE 1 = 1;
	DELETE FROM sys_automated_todo_action WHERE 1 = 1;
	DELETE FROM sys_field_value_action WHERE 1 = 1;
	DELETE FROM sys_notification_action WHERE 1 = 1;
	DELETE FROM sys_schedule_purge_action WHERE 1 = 1;
	DELETE FROM sys_rule WHERE 1 = 1;
	DELETE FROM sys_workflow WHERE 1 = 1;
	DELETE FROM sys_user_role WHERE 1 = 1;
	DELETE FROM sys_permission WHERE 1 = 1;
	DELETE FROM sys_role_permission WHERE 1 = 1;
	DELETE FROM sys_role_filter WHERE 1 = 1;
	DELETE FROM sys_list WHERE 1 = 1;
	DELETE FROM sys_listitem WHERE 1 = 1;
	DELETE FROM sys_grid_column WHERE 1 = 1;
	DELETE FROM sys_grid_data_filter WHERE 1 = 1;
	DELETE FROM sys_grid_data_filter_child WHERE 1 = 1;
	DELETE FROM sys_grid_filter WHERE 1 = 1;
	DELETE FROM sys_flag WHERE 1 = 1;
	DELETE FROM sys_entity_evaluator WHERE 1 = 1;
	DELETE FROM isight_entity WHERE 1 = 1;
	DELETE FROM isight_field WHERE 1 = 1;
	DELETE FROM isight_dynamic_entity_field WHERE 1 = 1;
	DELETE FROM isight_dynamic_entity WHERE 1 = 1;
	DELETE FROM sys_document_action WHERE 1 = 1;
	DELETE FROM sys_layout WHERE 1 = 1;

> Save this file. 


### Step 9:
In your terminal, open a new tab/window inside your project’s directory. 

### Step 10:
Enter Postgres by using the command:   `psql -U postgres -d isight`  

### Step 11:
Now, run all of the DELETE lines from your `delete.txt` file in this window. 
> You may need to run them in groups, as my terminal was crashing trying to run them all at once.  

### Step 12:
Now open a tab in your terminal in the config directory for your project, and then run the entirety of the `cat.txt` file.
> Just copy the contents of the file with `CMD+A`, `CMD+C`, then `CMD+V` to paste it in your terminal and run it.
   
Once this has completed, run:

	make migrate DISABLE_DB_BACKUP=true
	make sync-dynamic-forms
	make sync-translations
	make sync-permissions
	make sync-user-roles
	make sync-picklists

### Step 13:
After this point, the last thing you need to do is reassign the correct **user-role-id** to your Test user.

> I do this by opening Postico, finding the **id** for the _**Super User user-role**_, copying it,
> and pasting it directly into the **user-role-id** field in the **sys_user** table for the Test user,
> then clicking Save. It’s a janky way to do things, but it works for me.  

### Step 14:
Now if you run `make watch`, and `node server`, you should essentially have a cloned version of the PROD application running on your local.
   
