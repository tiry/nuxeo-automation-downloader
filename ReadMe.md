nuxeo-automation-downloader
===========================

## About this module

This module overrides the `Seam.Download` operation and provide an alternate Download Servlet.

## Why this module

In the default implementation the `Seam.Download` operation uses the Seam/JSF stack to handle Blob Downloads.

As a result, the download goes through the buffering `ResponseWrapper` set by the JSF stack : this can cause memory issues.

## How to works

The overriding `Seam.Download` does a specific processing for files biger that 5 MB :

 - store reference of the Blob in Session
 - redirect to a custom Servlet
 - the servlet will download the Blob and cleanup the Session

## Building 

    mvn clean install

## Using

The bundle will replace the default `Seam.Download` operation, so all you have to do is :

 - to copy the bundle in `nxserver/plugins` or `nxserver/bundles`
 - restart the server

After restart, the `Seam.Download` operation will use the new implementation.

