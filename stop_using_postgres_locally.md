## Using Postgres locally can often cause the quartz container to consistently crash

This can be avoided by Stopping Postgres from running (it usually starts automatically at startup)

![Screen Shot 2024-05-03 at 3 30 02 PM](https://github.com/CExKForsyth/Kyles-Case-IQ-Notes/assets/95767293/e1ca16da-d3de-4822-9660-a39f83adf2fc)

Once you've stopped Postgres, and you rerun `make setup`, watch the Quartz container in Docker Desktop to see if it crashes, if so, restart it quickly. It should continue to stay running from now on. 

![Screen Shot 2024-05-03 at 3 28 44 PM](https://github.com/CExKForsyth/Kyles-Case-IQ-Notes/assets/95767293/3757c5da-0639-43ff-860a-0976a01db150)

If you need to run SQL commands in postgres, you wont be able to do so from your Terminal now, but rather, you can use Docker Desktop

Click on the name of the postgres container

![Screen Shot 2024-05-03 at 3 35 01 PM](https://github.com/CExKForsyth/Kyles-Case-IQ-Notes/assets/95767293/0225512d-b3dd-40b0-bf67-a233c4a4d417)

Click Terminal

![Screen Shot 2024-05-03 at 3 35 22 PM](https://github.com/CExKForsyth/Kyles-Case-IQ-Notes/assets/95767293/e3632b9b-5425-4dc1-8c0c-19f7f0ab12b3)

Run this command:
`psql -U postgres -d isight`

![Screen Shot 2024-05-03 at 3 35 42 PM](https://github.com/CExKForsyth/Kyles-Case-IQ-Notes/assets/95767293/79665175-ee19-4bdb-a139-b30bec4a4f4f)

Now you can run any SQL commands you need to run here. (Or in Postico)
