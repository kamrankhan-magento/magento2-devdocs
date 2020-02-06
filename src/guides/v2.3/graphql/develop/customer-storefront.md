---
group: graphql
title: Customer Storefront API
---

The Magento 

## High-level goals

*  Support move toward microservice architecture

*  Decouple storefront business logic into individual services

*  Improve performance for storefront scenarios

*  Independent releases

Desired State Requirements

## Decoupling

The Storefront application must be decoupled from Magento; it may depend on Magento framework.
The Connector application must be separate application from Magento and Storefront; it may depend on Magento framework.
The Magento monolith application must not be dependent on the Storefront or Connector application.

## Reliability

The Storefront service must continue to operate in the case that Magento is down.
The Magento monolith should continue to operate in the case that the Storefront service is down.
Both Magento and Storefront should continue to operate in the case that the data communication infrastructure (i.e. message queues) is down.
Data should be kept in-sync between monolith and storefront and be eventually consistent.

## Product

Customer storefront application must be releasable as an independent package.
The Storefront application must define an API for managing it's entities (i.e. Storefront API).
GraphQl schema must remain backward compatible.

## Initial Version Requirements

Create a Customer SF Extension that can be packaged and released independently from Monolith
SF Extension should contain Storefront API/App, Connector, Synchronizer, and GraphQl schema/resolvers
SF Extension can be installed alongside Magento monolith in the same manner as current extensions
The SF Extension must not be dependent on any Magento modules; it may only depend on Magento/Framework
Exceptions??? The Integration module to handle authentication (for initial version only, with plans to resolve dependency later)
SF Extension will define it's own datastore and not rely on Magento tables directly (initially SF data store may be it's own tables in the same database as core)
Communication (data synchronization) between Monolith and Storefront should work asynchronously over message queues, and through the Connector
Data should be kept in-sync between monolith and storefront and be eventually consistent.
The Storefront application must define an API for managing it's entities (i.e. Storefront API).
GraphQl schema must remain backward compatible.
TODO clarify requirement about handling conflicts for initial version

## Customer storefront database



### storefront_customer table


```sql
CREATE TABLE `storefront_customer` (
  `storefront_row_id` bigint(20) unsigned NOT NULL AUTO_INCREMENT COMMENT 'ID',
  `customer_document` json NOT NULL COMMENT 'Customer Entity data store',
  `email` varchar(255) GENERATED ALWAYS AS (json_unquote(json_extract(`customer_document`,'$.email'))) STORED,
  `website_id` varchar(255) GENERATED ALWAYS AS (json_unquote(json_extract(`customer_document`,'$.website_id'))) STORED,
  `customer_id` int(11) GENERATED ALWAYS AS (json_unquote(json_extract(`customer_document`,'$.id'))) STORED,
  PRIMARY KEY (`storefront_customer_id`),
  UNIQUE KEY `STOREFRONT_CUSTOMER_ENTITY_EMAIL_WEBSITE_ID` (`email`,`website_id`),
  UNIQUE KEY `XYZ_STOREFRONT_CUSTOMER_ENTITY_CUSTOMER_ID` (`customer_id`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8 COMMENT='Data';
```

### storefront_customer_address table


```sql

CREATE TABLE `storefront_customer_address` (
  `customer_address_row_id` bigint(20) unsigned NOT NULL AUTO_INCREMENT COMMENT 'ID',
  `customer_address_document` json NOT NULL COMMENT 'Customer Address Entity data store',
  PRIMARY KEY (`customer_address_row_id`)
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8 COMMENT='Data';
```