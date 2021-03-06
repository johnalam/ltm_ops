# ltm_ops
Angular.js app for F5 LTM operations.  initially provide CRUD for iRule Data-groups.  May be expanded to other to additional operations.
This app is composed of an Angular based UI, API operations, and a Big-IP tmsh script that must be loaded on the device.  A REST API call to the Big-IP runs the script. The script receives a command, the name of a data-group and, one or more records via the API call.  The script executes the command on the data-group with the records received.  The script can be found here:  https://github.com/johnalam/tmsh_datagroup_ops/

Operations supported as of this commit:
1) add/edit/delete data-group
2) add/edit/delete record within a datagroup

In addition to a web server, the app relies on a reverse proxy to forward API calls to the F5 device.  The reverse proxy is needed to get around CORS restrictions by the browser.  I used nginx for both web server and reverse proxy.  The IP address of the F5 devices being managed is passed to the reverse proxy via a header named 'target'.

You will need to install nginx.  The nginx configuration is in the nginx directory.

You can host the app on any web server but, since the API calls are sent to the same hostname, the web server must also reverse proxy.  If you change the hostname on the API request, the browser will raise a CORS violation.
