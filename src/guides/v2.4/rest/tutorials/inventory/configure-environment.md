---
layout: tutorial
title: Step 1. Configure your environment
subtitle: Order processing with Inventory Management
menu_title: Step 1. Configure your environment
menu_order: 10
level3_subgroup: msi-tutorial
return_to:
  title: REST Tutorials
  url: rest/tutorials/index.html
functional_areas:
  - Integration
---

This step guides you through the process of configuring your Magento instance so that you can perform the Order Processing with Inventory Management tutorial.

## Create two websites

**Sales Channels** are entities from which you sell inventory. You can set up Magento websites to be sales channels, and Magento supports extensions for creating other types of channels.

In this tutorial, we'll create the infrastructure needed to implement a US and a German store.

### Create the North America website

1. Log in to Admin and select **Stores** > Settings > **All Stores**. Click **Create Website**, then assign the following values:

   Field | Value
   --- | ---
   Name | North America Site
   Code | `na_site`

   Click **Save Web Site**.

1. Click **Create Store** and assign the following values:

   Field | Value
   --- | ---
   Web Site | North America Site
   Name | North America Store
   Code | `na_store`
   Root Category | Default Category

   Click **Save Store**.

1. Click **Create Store View** and assign the following values:

   Field | Value
   --- | ---
   Store | North America Store
   Name | US Store View
   Code | `us`
   Status | Enabled

   Click **Save Store View**.

### Create the Europe website

1. Select **Stores** > Settings > **All Stores** and click the **Create Website** button. Assign the following values:

   Field | Value
   --- | ---
   Name | Europe Site
   Code | `eu_site`

   Click **Save Web Site**.

1. Click **Create Store** and assign the following values:

   Field | Value
   --- | ---
   Web Site | Europe Site
   Name | Europe Store
   Code | `eu_store`
   Root Category | Default Category

   Click **Save Store**.

1. Click **Create Store View** and assign the following values:

   Field | Value
   --- | ---
   Store | Europe Store
   Name | Germany Store View
   Code | `de`
   Status | Enabled

   Click **Save Store View**.

## Configure website URLs (Optional)

To make it easier to locate products and log in as a customer later in this tutorial, configure Magento to add the store code to the URL.

1. Click **Stores** > Setting* > **Configuration** > **Web** and expand the **Url Options** section.
1. Change the value of **Add Store Code to Urls** to **Yes**.
1. Click **Save Config**.

## Configure payment and shipping methods

For this tutorial, we'll assume that payment and shipping methods are configured globally. You can also make configuration changes at the website or store view level.

### Set the payment method {#set-payment}

{% include webapi/tutorials/set-payment-methods.md %}

### Configure supported shipping methods and enable in-store delivery {#ship-method}

If an order contains one or more simple, configurable, bundle, or group products, then the customer must either specify a shipping method or select a location from which to pick up the order.

Downloadable and virtual products cannot be shipped, and Magento does not calculate shipping charges for these items.

Since we are not actually shipping any products in this tutorial, we do not need to set up an account with a shipping company such as UPS or Federal Express. Instead, we can use the offline shipping methods that are configured by default.

Delivery method | Configuration name | Enabled by default?
--- | --- | ---
Flat rate | `flatrate` | Yes
Table rate | `tablerate` | Yes
Free shipping | `freeshipping` | No
In-store delivery | Not applicable | No

To change which offline delivery methods are available:

1. Select **Stores** > Settings > **Configuration** > **Sales** > **Delivery Methods** in Admin.
1. Enable in-store delivery and adjust the status of the other delivery methods as desired.
1. Click **Save Config**.

## Reindex and flush the cache

**Required:** Perform a full reindex and flush the cache.

```bash
bin/magento indexer:reindex && bin/magento cache:flush
```

## Verify this step

Click **Stores** > Settings > **All Stores**. The websites, stores, and store views are displayed in the grid.
