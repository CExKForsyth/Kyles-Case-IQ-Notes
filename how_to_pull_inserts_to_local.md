# How to Recreate a PROD Environment Locally

### Step 1: Pull Inserts

To pull inserts and recreate a project env locally, we first run a `make setup` to set up our project locally, as usual.

In order to properly recreate the environment locally, we also need to login to Teleport and grab data from each of the following tables:
 
		`'sys_workflow'
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
		'sys_layout',`

We can do this by completing the next series of steps:   
In the db container for your project, navigate to `/var/isight/backup`  
`cd /var/isight/backup/` 
run the command: `ls` 

if you don’t see an `external-dumps` directory, 
run the command: `mkdir external-dumps`  

Great, now navigate to the service box and docker exec into the worker.   
You will need to run each of the following list of commands to strip files from the db in order to recreate the environment locally.   

>>Make sure you update each of these commands with the current date, for example if its **November 8th, 2023**, I would update the filename in each to: **sys_workflow_2023-11-08-231108.sql** 
>>Please use a code editor to change the name, make your life easier.  

`PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_workflow isight > /usr/local/data/db/external-dumps/sys_workflow_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_translation isight > /usr/local/data/db/external-dumps/sys_translation_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_state isight > /usr/local/data/db/external-dumps/sys_state_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_transition isight > /usr/local/data/db/external-dumps/sys_transition_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_condition isight > /usr/local/data/db/external-dumps/sys_condition_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_condition_type isight > /usr/local/data/db/external-dumps/sys_condition_type_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_filter isight > /usr/local/data/db/external-dumps/sys_filter_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_filter_child isight > /usr/local/data/db/external-dumps/sys_filter_child_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_filter_group isight > /usr/local/data/db/external-dumps/sys_filter_group_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_assignment_action isight > /usr/local/data/db/external-dumps/sys_assignment_action_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_document_action isight > /usr/local/data/db/external-dumps/sys_document_action_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_permission isight > /usr/local/data/db/external-dumps/sys_permission_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_automated_todo_action isight > /usr/local/data/db/external-dumps/sys_automated_todo_action_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_field_value_action isight > /usr/local/data/db/external-dumps/sys_field_value_action_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_notification_action isight > /usr/local/data/db/external-dumps/sys_notification_action_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_schedule_purge_action isight > /usr/local/data/db/external-dumps/sys_schedule_purge_action_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_rule isight > /usr/local/data/db/external-dumps/sys_rule_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_workflow isight > /usr/local/data/db/external-dumps/sys_workflow_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_user_role isight > /usr/local/data/db/external-dumps/sys_user_role_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_role_permission isight > /usr/local/data/db/external-dumps/sys_role_permission_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_role_filter isight > /usr/local/data/db/external-dumps/sys_role_filter_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_list isight > /usr/local/data/db/external-dumps/sys_list_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_listitem isight > /usr/local/data/db/external-dumps/sys_listitem_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_grid_column isight > /usr/local/data/db/external-dumps/sys_grid_column_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_grid_data_filter isight > /usr/local/data/db/external-dumps/sys_grid_data_filter_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_grid_data_filter_child isight > /usr/local/data/db/external-dumps/sys_grid_data_filter_child_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_grid_filter isight > /usr/local/data/db/external-dumps/sys_grid_filter_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_flag isight > /usr/local/data/db/external-dumps/sys_flag_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_entity_evaluator isight > /usr/local/data/db/external-dumps/sys_entity_evaluator_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=isight_entity isight > /usr/local/data/db/external-dumps/isight_entity_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=isight_field isight > /usr/local/data/db/external-dumps/isight_field_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=isight_dynamic_entity_field isight > /usr/local/data/db/external-dumps/isight_dynamic_entity_field_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=isight_dynamic_entity isight > /usr/local/data/db/external-dumps/isight_dynamic_entity_2023-09-28-115027.sql 
PGPASSWORD= pg_dump --column-inserts --data-only -h db -p 5432 -U postgres  --table=sys_layout isight > /usr/local/data/db/external-dumps/sys_layout_2023-09-28-115027.sql` 

After running each of these from the worker, go back to the db box, and navigate to the external-dumps directory from earlier.   

Run this command: `ls -halt`  

You should now see all the files you just created from the worker.  
￼
Next step, we compile them into a zip file. 
This is where the date is important.   
From this directory, run the following command to create a zip file, but use the same date as the created files:
`find *2023-10-30* -exec tar -rvf archive-oct-30-b.tar.gz {} --strip-components=1 \;`  
>>make sure to also change the date in the archive file name to match the date of the field as well  

Now download the created zip file.  
Once downloaded, unzip the file, and keep this directory on your desktop.   

Now open the directory in VSCODE.
￼
Create a new file at the base of the directory called `script.js`  In this file, add this code:  

`const fs = require('fs');
fs.readdir('./', (error, files) => {
console.log('files:', files);
files.forEach(file => {
    if(file.includes('.sql')){
        console.log(``cat /Users/kforsyth/Desktop/archive-oct-30-b/${file} | PGPASSWORD=postgres  psql  -h 127.0.0.1 -p 5432 -U postgres --set ON_ERROR_STOP=on isight``);
    }
})
});`
>>Again, change the path the match your path, with your computer’s username, and the correct archive zip file name.

Now create a new empty file in the base of the directory called `cat.txt`  

Open the VSCode terminal, and from the base of this directory, run: `node script.js`  
Copy the entire result from your terminal, and past the entire result into `cat.txt`. 
Save this file.  
Now create another new file in the base of the directory called `delete.txt`  
Paste all of these queries into it:  

`DELETE FROM sys_workflow WHERE 1 = 1;
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
DELETE FROM sys_layout WHERE 1 = 1;`

Save this file. 

Now we’re ready to recreate the environment locally.

In your terminal, open a new tab/window inside your project’s directory. 

Enter Postgres by using the command:   `psql -U postgres -d isight`  

Now, run all of the DELETE lines from your `delete.txt` file in this window. 
>>You may need to run them in groups, as my terminal was crashing trying to run them all at once.  

Once you’ve run these delete queries, the next step is to open a tab in your terminal in the config directory for your project, and then run the entirety of the `cat.txt` file.
>>Just copy the contents of the file with `CMD+A`, `CMD+C`, then `CMD+V` to paste it in your terminal and run it.
   
Once this has completed, run:  
`make migrate DISABLE_DB_BACKUP=true
make sync-dynamic-forms
make sync-translations
make sync-permissions
make sync-user-roles
make sync-picklists`

After this point, the last thing you need to do is reassign the correct user-role-id to your test user.

I do this by opening Postico, finding the **id** for the _**Super User user-role**_, copying it,
and pasting it directly into the **user-role-id** field in the **sys_user** table for the Test user,
then clicking Save. It’s a janky way to do things, but it works for me.  

Now if you run `make watch`, and `node server`, you should have essentially a cloned version of the application on your local.
   
