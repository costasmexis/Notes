# Saturn Cloud Quickstart
Saturn Cloud is a data science platform that helps people quickly do work using whatever technology they need, including high-memory computing, GPU processors, and Dask clusters. You can use Saturn Cloud with Python, R, or nearly any other programming language.

## Start a resource
Once a resource is created, you’ll need to turn it on. Press the blue **Start** button on the resource’s page to start the server.
As your machine starts up, the card will display _pending_, and you will see a progress bar showing the steps and overall progress toward starting the server.
Once you’re in the IDE, you can write, run, and save code. You can also connect your resource to git repositories to version control your code.

## Stop the resource
When you’re done using the resource, shut it down by clicking the red **Stop** button on the card. 

***SOS***: By default, the resource will automatically shut off after the browser window has been inactive for an hour (this only applies to some resource types).

# Auto-Shutoff
How Saturn Cloud resources automatically turn off after inactivity

_Auto-shutoff_ is a setting that sets a period of time of inactivity after which a Jupyter server will automatically shut down. **This can prevent you from wasting money on expensive resources that are accidentally left on.** When Jupyter and RStudio servers are created, you can choose an auto-shutoff period. This defaults to 1 hour, but you can also select 6 hours, 3 days, 7 days, or never. After a period of inactivity of the set length, the resource will automatically shut off.

-   **Jupyter Server** - A Jupyter server resource is running if either (1) a browser window for JupyterLab is open or (2) an SSH connection is open to the resource. For modern browsers having a laptop go to sleep will disconnect the browser window and ssh connections, thus starting the idle timer.

