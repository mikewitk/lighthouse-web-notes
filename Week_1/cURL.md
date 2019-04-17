# cURL

cURL is a command line utility that is used to make HTTP requests to a given URL and it outputs the response.

1. Downlaod a Single File

`curl http://www.centos.org > centos-org.html`

2. Save the cURL Outupt to a file

We can save the result of the curl command to a file by using -o/-O options

* -o the result will be saved in the filename provided in the command line
* -O the filename in the URL will be taken and it will be used as the filename to store the result

`$ curl -o mygettext.html http://www.gnu.org/software/gettext/manual/gettext.html`

Now the page gettext.html will be savend in the file named 'mygettext.html'

3. Fetch Multiple Files at a Time

`curl -O URL1 -O URL2`

4. Follow HTTP Location Headers with L-Option

By default cURL doesn't follow the HTTP Location headers.

For example, when someone types 'google.com' in the browser from India, it will be automatically redirected to 'google.co.in'. This is done based on the HTTP Location header.

5. Continue/Resume a Previous Download

`curl -C - -O <URL>`

6. Limit the Rate of Data Transfer

`curl --limit-rate 1000B -O <URL`

7. Donwload a file only if it's modified before/after the given time

Below command will donwload only if it is modifed later than the given date and time
`curl -z 21-Dec-11 <URL>`

Below command will download if it is modified efore than tthe given date and time
`curl -z -21-Dec-11 <URL>`

8. Pass HTTP Authentication in cURL

`curl -u username:password URL`

