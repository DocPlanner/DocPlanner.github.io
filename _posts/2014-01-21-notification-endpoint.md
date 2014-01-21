---
layout: default
title: Notification endpoint
categories: [en]
---

Notification endpoint
=====================

To docplanner database up to date with an external data source it’s best for the 3rd party to send notifications to docplanner about changing of visit status.

Our REST API provides all necessary methods but for your convinience, there is also a SOAP endpoint with only two methods, and better documentation.

WSDL is located at: [http://www.znanylekarz.pl/soap/wsdl.xml](http://www.znanylekarz.pl/soap/wsdl.xml)


Description
===========

There are two methods published: `VisitBook` and `VisitCancel`. They both require same parameters:

  * `token` -- this is a string used for authorization, provided by docplanner
  * `visitId` -- this is a string indentifying a visit in 3rd party system. As you may have noticed, this is not a number/integer, so it’s possible to use composite value (for exampe: facility_id/slot_id) or some other complex type (json for instance, etc). 

There is no sensitive data exchanged. Docplanner will fetch the details about this visit and synchronize data accordingly.
