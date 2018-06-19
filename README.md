examples
--------

to run: `docker-compose up`

credentials
-----------

username: `test:tester`
password: `testing`

swift api example
-----------------

    $ curl -i -H "x-auth-user: test:tester" -H "x-auth-key: testing" http://localhost:8080/auth/v1.0
    HTTP/1.1 200 OK
    X-Storage-Url: http://localhost:8080/v1/AUTH_test
    X-Auth-Token-Expires: 86399
    X-Auth-Token: AUTH_tk8582e3deeddd49f6b85e4dd2ac381099
    Content-Type: text/html; charset=UTF-8
    X-Storage-Token: AUTH_tk8582e3deeddd49f6b85e4dd2ac381099
    Content-Length: 0
    X-Trans-Id: txbaee3b15157e4121903dd-005b11dcb2
    X-Openstack-Request-Id: txbaee3b15157e4121903dd-005b11dcb2
    Date: Fri, 01 Jun 2018 23:54:26 GMT

    $ curl -i -H "X-Auth-Token: AUTH_tk8582e3deeddd49f6b85e4dd2ac381099" http://localhost:8080/v1/AUTH_test
    HTTP/1.1 200 OK
    Content-Length: 7
    X-Account-Storage-Policy-Policy-0-Bytes-Used: 12
    X-Account-Object-Count: 2
    X-Account-Meta-Foo: bar
    X-Account-Storage-Policy-Policy-0-Container-Count: 2
    X-Timestamp: 1525214842.86156
    X-Account-Storage-Policy-Policy-0-Object-Count: 2
    X-Account-Bytes-Used: 12
    X-Account-Container-Count: 2
    Content-Type: text/plain; charset=utf-8
    Accept-Ranges: bytes
    X-Trans-Id: txafb433b63375469280128-005b11dcc0
    X-Openstack-Request-Id: txafb433b63375469280128-005b11dcc0
    Date: Fri, 01 Jun 2018 23:54:40 GMT

    c
    test
    $ curl -i -H "X-Auth-Token: AUTH_tk8582e3deeddd49f6b85e4dd2ac381099" http://localhost:8080/v1/AUTH_test/c/o
    HTTP/1.1 200 OK
    Content-Length: 4
    Accept-Ranges: bytes
    Last-Modified: Wed, 23 May 2018 22:38:55 GMT
    Etag: 81dc9bdb52d04dc20036dbd8313ed055
    X-Timestamp: 1527115134.93637
    X-Object-Meta-Foo: bar
    Content-Type: application/x-www-form-urlencoded
    X-Trans-Id: tx30449bac6d9943d7bbc68-005b11dcc7
    X-Openstack-Request-Id: tx30449bac6d9943d7bbc68-005b11dcc7
    Date: Fri, 01 Jun 2018 23:54:47 GMT

    1234

s3 api example
--------------

    $ cat .s3cfg
    [default]
    access_key = test:tester
    bucket_location = US
    host_base = localhost:8080
    host_bucket = %(bucket)s.localhost:8080
    secret_key = testing
    use_https = False
    $ s3cmd get s3://test/test.yaml testyaml2
    download: 's3://test/test.yaml' -> 'testyaml2'  [1 of 1]
     106 of 106   100% in    0s     2.18 kB/s  done
    $ s3cmd ls
    2009-02-03 16:45  s3://test
    $ s3cmd ls s3://test
    2018-06-01 22:47       106   s3://test/test.yaml
    $ s3cmd get s3://test/test.yaml testyaml
    download: 's3://test/test.yaml' -> 'testyaml'  [1 of 1]
     106 of 106   100% in    0s  1764.61 B/s  done
    $ md5sum test.yaml testyaml
    ece048c58129296893191a17ee3dbe66  test.yaml
    ece048c58129296893191a17ee3dbe66  testyaml


logging
-------

to check logs: `docker logs -f syslog`. These logs are buffered.
