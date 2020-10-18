# GonderiTakibi

**IMPORTANT: Project Is Deprecated!**
> tracking and logging your shipments for international PTT posts.

![Screenshot](https://raw.githubusercontent.com/Shavell/repo-assets/master/gonderiTakibi/tracking.gif)

## Example of Essential SQL Queries

> Return all result with definition and tracking code!

```` 
select la.tracking_code_id,
       r.last_process_comment,
       r.last_process_date,
       r.total_fees,
       tc.definition,
       r.delivery_comment
from main.log_result r
         join log_action la on r.log_action_id = la.id
         left join tracking_code tc on la.tracking_code_id = tc.tracking_id
````

>If u need only having fee packages u can execute this query
````
select la.tracking_code_id,
       r.last_process_comment,
       r.last_process_date,
       r.total_fees,
       tc.definition,
       r.delivery_comment
from main.log_result r
         join log_action la on r.log_action_id = la.id
         left join tracking_code tc on la.tracking_code_id = tc.tracking_id
where r.total_fees is not null
````

>If u need last result of tracking
````
select la.tracking_code_id,
       r.last_process_comment,
       r.last_process_date,
       r.total_fees,
       tc.definition,
       r.delivery_comment
from main.log_result r
         join log_action la on r.log_action_id = la.id
         left join tracking_code tc on la.tracking_code_id = tc.tracking_id
where la.log_test_transaction_id = (select id from log_test_transaction order by id desc limit 1)
order by r.last_process_date asc
````

> Sqlite3-cli result for related query 
![SQLOUTPUT](https://raw.githubusercontent.com/Shavell/repo-assets/master/gonderiTakibi/sqlite-cli.PNG)


## How to use

 - Make sure you are using python 3.6 (conda will help you)
 - Firstly pip install -r requirements.txt
 - Open db/models.py and edit example section for own requirements.
 - Run db/models.py for creation tables to sqlite.db
 - if ur mllib models is ready for actions, u can start application with main.py


## Requirements
- Python 3.6
- ChromeDriver for chrome
- PhantomJS (Optional)
- Trained captcha recognizer model (i don't share my trained model, I believe you can do it)


## License

The gonderiTakibi is open-sourced software licensed under the [GPL-3.0 license](https://opensource.org/licenses/MIT).
